<template>
  <div id="app">
    <main>
      <center>
        <img src="@/assets/Pokemon_Ruby.webp" width="200" alt="" />
        <h1 class="title" style="color:white">Pokedex</h1>
        <hr />
      </center>
      <Screen msg="Welcome to Your Vue.js App" /> <br /><br />
      <div class="music-player has-text-centered">
        <audio
          ref="audio"
          src="@/assets/ruby_opening.ogg"
          preload
          loop
          id="audio"
        ></audio>
        <div
          @click="toggleSound()"
          class="toggle-sound button is-light is-outlined"
        >
          Toggle Main Menu Music
        </div>
      </div>
      <br /><br />
      <center>
        <small style="color: white"
          >Made with 💜 and ☕ by
          <a style="color: white" href="https://emk.dev">Eric Kelley</a></small
        >
      </center>
    </main>
  </div>
</template>

<script>
import Screen from "./components/Screen.vue";

export default {
  name: "App",
  components: {
    Screen,
  },
  methods: {
    toggleSound() {
      let audio = this.$refs.audio;
      audio.volume = 0.15;
      if (audio.paused || !audio.currentTime) {
        console.log("play");
        audio.play();
      } else {
        console.log("pause");
        audio.pause();
      }
    },
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
}
#app {
  color: #2c3e50;
  background: radial-gradient(#a51818, #620e0e);
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-smooth: never;
}
@font-face {
  font-family: "Pokemon Pixel";
  src: local("Pokemon Pixel Font"),
    url(./assets/Pokemon-Pixel-Font.woff) format("woff2"),
    url(./assets/Pokemon-Pixel-Font.woff) format("woff");
}
</style>
