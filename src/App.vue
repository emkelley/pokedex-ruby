<template>
  <div id="app">
    <main>
      <center>
        <img src="@/assets/Pokemon_Ruby.webp" width="200" alt="" />
        <h1 class="title" style="color:white">Pokedex</h1>
        <hr />
      </center>
      <Screen msg="Welcome to Your Vue.js App" />
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
};
</script>

<style lang="scss">
body {
  margin: 0;
}
#app {
  color: #2c3e50;
  background-color: #675e9d;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
@font-face {
  font-family: "Pokemon Pixel";
  src: local("Pokemon Pixel Font"),
    url(./assets/Pokemon-Pixel-Font.woff) format("woff2"),
    url(./assets/Pokemon-Pixel-Font.woff) format("woff");
}
</style>
