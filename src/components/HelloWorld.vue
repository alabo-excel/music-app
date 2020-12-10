<template>
  <div class="hello">
    <div>
      <div class="p-3 bg-primary text-white"><h1>My Music App</h1></div>
      <b-card-group deck>
        <b-card footer-tag="footer">
          <template>
            <div class="d-flex justify-content-center">
              <h5 class="mb-0">{{ current.title }}</h5>
              - <span> {{ current.artist }}</span>
            </div>
            <div  class="d-flex justify-content-between my-4">
              <b-icon @click="prev" icon="arrow-left-square-fill"></b-icon>
              <b-icon @click="play" v-if="!isPlaying" icon="play-fill"></b-icon>
              <b-icon @click="pause" icon="pause-fill" v-else></b-icon>
              <b-icon @click="next" icon="arrow-right-square-fill"></b-icon>
            </div>
          </template>
          <b-button class="text-left m-1 d-flex justify-content-between" v-for="song in songs" :key="song.title" variant="outline-primary" @click="play(song)">{{ song.title }} <p> {{song.artist}}</p> </b-button>
        </b-card>
      </b-card-group>
            <div class="p-3 bg-primary text-white"><h6>Alabo Excel 2020</h6></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      index: 0,
      current: {},
      isPlaying: false,
      songs: [
        { title: "20 10 10", artist: "Burna Boy", src: require("../assets/20_10_20.mp3") },
        { title: "Champion", artist: "Fire Boy DML", src: require("../assets/champion.mp3") },
        { title: "Johnny", artist: "Falz", src: require("../assets/Johnny.mp3") },
        { title: "Twice As Tall", artist: "Burna Boy", src: require("../assets/Level_Up_Twice_As_Tall.mp3") },
        { title: "Monsters You Made", artist: "Burna Boy", src: require("../assets/Monsters_You_Made.mp3") },
      ],
      player: new Audio(),
    };
  },
  methods: {
    play(songs) {
      if (typeof songs.src != "undefined") {
        this.current = songs;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++
      if(this.index > this.songs.length -1){
        this.index = 0
      }
      this.current = this.songs[this.index];
      this.play(this.current); 
    },
    prev() {
      this.index--
      if(this.index < 0){
        this.index = this.songs.length -1
      }
      this.current = this.songs[this.index];
      this.play(this.current);     },
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    // this.player.play();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.btn-outline-primary{
  width: 100%;
}
</style>
