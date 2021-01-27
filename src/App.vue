<template>
  <div id="app">
    <main>
      <div class="level">
        <div class="level-left">
          <div class="level-item">
            <div>
              <img src="@/assets/Pokemon_Ruby.webp" width="200" alt="" />
              <br /><br />
            </div>
          </div>
        </div>
        <div class="level-right">
          <div class="level-item">
            <div>
              <h1 class="title" style="color:white">Project Pokédex - Ruby</h1>
              <br />
              <small style="color: white; float: right"
                >Made with 💜 and ☕ by
                <a style="color: white" href="https://emk.dev"
                  >Eric Kelley</a
                ></small
              >
            </div>
          </div>
        </div>
      </div>
      <center>
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
          Toggle Pokémon Ruby Menu Theme
        </div>
      </div>
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
