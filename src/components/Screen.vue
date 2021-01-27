<template>
  <div id="screen" ref="content">
    <button class="button" @click="renderToPDF()">screenshot</button>
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
          <div
            class="previous"
            v-for="pokemon in pokemonNames"
            :key="pokemon.id"
          >
            <img
              :id="pokemon.id"
              :src="getSpriteURL(pokemon.id)"
              :class="{ 'is-first': pokemon.id === 1 }"
              width="100%"
              alt=""
            />
          </div>
        </div>
      </div>
      <div class="column scrollable-list">
        <div class="scrollable-list--container">
          <ul id="pokemonList" v-if="pokemonNames">
            <li
              v-for="pokemon in pokemonNames"
              :key="pokemon.id"
              @click="setActive(pokemon.id)"
              :id="getListItemID(pokemon.id)"
              :class="{ 'is-first is-active': pokemon.id === 1 }"
            >
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
import jsPDF from "jspdf";
import domtoimage from "dom-to-image";
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
    getSpriteURL(id) {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/ruby-sapphire/${id}.png`;
    },
    getListItemID(id) {
      return `pokemon-${id}`;
    },
    setActive(id) {
      const activeSprite = document.getElementById(id);
      const activeListItem = document.getElementById(`pokemon-${id}`);
      activeListItem.scrollIntoView({ block: "center" });
      activeSprite.scrollIntoView({ behavior: "smooth", block: "center" });
      this.toggleClasses(activeListItem);
    },
    toggleClasses(newActiveItem) {
      const oldActive = document.getElementsByClassName("is-active")[0];
      oldActive.classList.toggle("is-active");
      newActiveItem.classList.toggle("is-active");
    },
    renderToPDF() {
      domtoimage
        .toPng(this.$refs.content)
        .then((imgData) => {
          let img = new Image();
          img.src = imgData;
          const doc = new jsPDF("l", "mm", "letter");
          doc.addImage(img, "JPEG", 10, 10);
          doc.save("screenshot-pdf");
          console.error(doc);
        })
        .catch(function(error) {
          console.error("oops, something went wrong!", error);
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#screen {
  outline: 8px solid black;
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
  text-shadow: 3px 2px #000000;
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
    box-shadow: 3px 2px #000000;
  }
  p {
    font-size: 5rem;
    font-weight: bold;
    letter-spacing: 0.3rem;
    text-shadow: 4px 3px #000000;
    font-smooth: never;
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
  overflow-y: scroll;
  background: linear-gradient(
      0deg,
      #9f9ea3 0%,
      rgba(0, 0, 0, 0) 23%,
      rgba(0, 0, 0, 0) 77%,
      #9f9ea3 100%
    ),
    white;

  &::-webkit-scrollbar-track {
    display: none;
  }

  &::-webkit-scrollbar {
    display: none;
  }

  &::-webkit-scrollbar-thumb {
    display: none;
  }
  img {
    image-rendering: pixelated;
    image-rendering: -moz-crisp-edges;
    image-rendering: crisp-edges;
    width: 200px;
    // margin-top: -3rem;
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
  user-select: none;
  cursor: pointer;
  span {
    margin-left: 0.5rem;
    text-transform: none;
    font-weight: bold;
    color: rgb(34, 34, 34);
  }
  .is-active {
    background: white;
    border-radius: 20px;
  }

  &::-webkit-scrollbar-track {
    background-color: transparent;
  }

  &::-webkit-scrollbar {
    width: 5px;
    background-color: transparent;
  }

  &::-webkit-scrollbar-thumb {
    background-color: #000000;
    border-top-left-radius: 4px;
    border-bottom-left-radius: 4px;
    margin-right: 1rem;
  }
}
.is-first {
  margin-top: 80%;
}
</style>
