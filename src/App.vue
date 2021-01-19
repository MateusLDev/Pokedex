<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h1 class="is-size-2">Pokedex</h1>

      <div class="search">
        <input type="text" placeholder="Nome Pokemon" class="input-search" v-model="search">
      </div>
      
      <div v-for="(pokemon, index) in resultSearch" :key="pokemon.url">
        <pokemon :num="index + 1" :name="pokemon.name" :url="pokemon.url" />
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import Pokemon from './components/Pokemon.vue';

export default {
  name: 'App',
  components:{
    Pokemon
  },
  data(){
    return{
      search: '',
      pokemons: []
    }
  }, 
  created() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results
    })
  },
  computed: {
    resultSearch(){
      if(this.search == '' || this.search == ' '){
        return this.pokemons
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.search)
      }
    }
  }
}
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

.search{
  border: 1px solid #000;
  border-radius: 20px;
  padding: 10px 15px;
  display: flex;
  justify-content: space-between;
  margin: 20px 0;
}

.search .input-search{
  border: none;
  width: 100%;
}
</style>
