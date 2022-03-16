<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <div>
        <input
          class="input is-rounded"
          type="text"
          placeholder="Buscar pokemon pelo nome"
          v-model="find"
        />
        <button id="buttonFind" class="button is-success" @click="search">Buscar</button>
      </div>
      <div v-for="(pokemon, index) in filteredPokemons" :key="pokemon.url">
        <Pokemon :name="pokemon.name" :url="pokemon.url" :index="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/PokemonItem";
export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons : [],
      find: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((response) => {
        this.pokemons = response.data.results;
        this.filteredPokemons = this.pokemons;
      });
  },
  components: {
    Pokemon,
  },
  methods:{
    search : function(){      
      if(this.find == '' || this.find == ' '){
        this.filteredPokemons = this.pokemons;
        return;
      }

      this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.find);
    }
  }
};
</script>
  

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#buttonFind {
  margin-top: 1%;
  margin-bottom: 1%;
}
</style>
