<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <div class="has-text-centered">
        <img src="./assets/pokemon_logo.png" />
        <hr />
        <h4 class="is-size-4">Pokedex</h4>
        <div class="field">
          <input
            type="text"
            class="input is-rounded"
            placeholder="Buscar pokemon pelo nome"
            v-model="busca"
          />
        </div>
        <div class="field is-grouped">
          <button class="button is-fullwidth is-primary is-rounded" @click="buscar">
           Buscar
          </button>
        </div>
      </div>

      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :num="index + 1" :url="poke.url" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";
export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    };
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    buscar: function() {
      this.filteredPokemons = this.pokemons;
       if (this.busca == "" || this.busca == "") {
         this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name.match(this.busca.toLocaleLowerCase()));       
      }
    }
  },
  computed: {
    /*
    resultadoBusca: function () {
      if (this.busca == "" || this.busca == "") {
        return this.pokemons;
      } else {
        return this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    },
    */
  },
};
</script>

<style>
</style>
