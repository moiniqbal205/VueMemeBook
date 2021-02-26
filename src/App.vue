<template>
  <div id="app">
    <nav class="navbar navbar-dark bg-dark">
      <h2>Meme<span>Book</span></h2>
    </nav>    
    <div>
      <b-carousel
        id="carousel-1"
        :interval="4000"
        controls
        indicators
        background="#2c3e50"
        style="text-shadow: 1px 1px 2px #333;"
      >
        <!-- Text slides with image -->
        <b-carousel-slide
          class="slider"
          v-for="(meme, index) in memes"
          :key="index"
          :caption="meme.name"
          :img-src="meme.url"
        ></b-carousel-slide>
      </b-carousel>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data () {
    return {
      memes: []
    }
  },
  mounted () {
    axios.get("https://api.imgflip.com/get_memes")
    .then(response => {
        this.memes = response.data.data.memes;
      });
  }
}
</script>

<style>

body {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

h2 {
  padding: 15px;
  width: 100%;
  color: #ccc;
}

h2 span {
  color: greenyellow;
}

.slider {
  background-repeat: no-repeat;
  background-position: center center;
  background-size: 100% 100%;
  width: 100%;
  height: auto;
}
</style>
