<template>
  <div id="screen">
    <div class="columns">
      <div class="column is-3 stats has-text-centered">
        <div class="stats--container">
          <h1 class="title">Seen</h1>
          <hr />
          <p>386</p>
          <h1 class="title">Own</h1>
          <hr />
          <p>386</p>
        </div>
      </div>
      <div class="column is-4 pokemon-wheel">
        <div class="pokemon-wheel--container pxl-border">
          <div class="previous">
            <img
              src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/ruby-sapphire/1.png"
              width="100%"
              alt=""
            />
          </div>
          <div class="current">
            <img
              src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/ruby-sapphire/4.png"
              width="100%"
              alt=""
            />
          </div>
          <div class="next">
            <img
              src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/ruby-sapphire/7.png"
              width="100%"
              alt=""
            />
          </div>
        </div>
      </div>
      <div class="column scrollable-list">
        <div class="scrollable-list--container">
          <ul v-if="pokemonNames">
            <li v-for="pokemon in pokemonNames" :key="pokemon.id">
              <span>No</span>{{ pad(pokemon.id, 3) }} {{ pokemon.name }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import pokemon from "pokemon";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      pokemonNames: undefined,
    };
  },
  mounted() {
    this.getPokemonList();
  },
  methods: {
    getPokemonList() {
      const allPokemonNames = pokemon.all();
      const gen3Names = allPokemonNames.slice(0, 386);
      const gen3NameObjects = [];
      gen3Names.forEach((name) => [
        gen3NameObjects.push({
          id: pokemon.getId(name),
          name: name,
        }),
      ]);
      this.pokemonNames = gen3NameObjects;
    },
    pad(number, length) {
      let str = "" + number;
      while (str.length < length) {
        str = "0" + str;
      }
      return str;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#screen {
  border: 5px solid black;
  background-image: linear-gradient(
    0deg,
    #595b5f 25%,
    #a09fa4 25%,
    #a09fa4 50%,
    #595b5f 50%,
    #595b5f 75%,
    #a09fa4 75%,
    #a09fa4 100%
  );
  background-size: 40px 40px;
  width: 800px;
  height: 600px;
  padding-top: 0.1rem;
  overflow: hidden;
}
.stats {
  font-family: "Pokemon Pixel";
  color: white;
  padding: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  text-shadow: 2px 2px #000000;
  .stats--container {
    width: 100%;
  }
  .title {
    color: white;
    font-size: 3rem;
    letter-spacing: 0.1rem;
    text-transform: uppercase;
    margin-bottom: 0;
  }
  hr {
    height: 5px;
    margin: 0;
    box-shadow: 2px 2px #000000;
  }
  p {
    font-size: 5rem;
  }
}
.pokemon-wheel {
  display: flex;
  align-items: center;
  height: 600px;
  padding: 0;
  padding-top: 1rem;
}
.pokemon-wheel--container {
  display: flex;
  align-items: center;
  flex-direction: column;
  border: 3px solid black;
  border-radius: 10px;
  height: 500px;
  width: 100%;
  overflow: hidden;
  background: linear-gradient(
      0deg,
      #9f9ea3 0%,
      rgba(0, 0, 0, 0) 23%,
      rgba(0, 0, 0, 0) 77%,
      #9f9ea3 100%
    ),
    white;
  img {
    image-rendering: pixelated;
    image-rendering: -moz-crisp-edges;
    image-rendering: crisp-edges;
    width: 250px;
    margin-top: -3rem;
  }
}
.scrollable-list {
  padding: 0;
  padding-top: 1.9rem;
  padding-bottom: 1rem;
  padding-left: 0.75rem;
  padding-right: 1rem;
}
.scrollable-list--container {
  background: #ffbf54;
  border: 3px solid black;
  border-radius: 10px;
  max-height: 555px;
  overflow-y: scroll;
  padding: 0.5rem;
  font-family: "Pokemon Pixel";
  font-size: 3rem;
  color: rgb(75, 75, 75);
  text-shadow: 2px 2px #e6e6e6;
  text-transform: uppercase;
  span {
    text-transform: none;
    font-weight: bold;
    color: rgb(34, 34, 34);
  }

  &::-webkit-scrollbar-track {
    background-color: #ffbf54;
  }

  &::-webkit-scrollbar {
    width: 13px;
    background-color: #ffbf54;
  }

  &::-webkit-scrollbar-thumb {
    background-color: #000000;
    border-top-left-radius: 4px;
    border-bottom-left-radius: 4px;
    margin-right: 1rem;
  }
}
</style>
