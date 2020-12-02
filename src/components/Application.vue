<template>
  <div>
    <div class="column is-half is-offset-one-quarter">
      <img src="../assets/pokedex.svg">
      <hr>
      <input class="input is-rounded is-info" type="text" placeholder="Busque um pokemon pelo nome" v-model="busca">
      
        <div class="buttons is-centered">
          <button class="button is-info is-medium" id="buscarBtn" @click="buscar">Buscar</button>
        </div>
          
      

      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1"/>   
      </div>
    </div>
  </div>
</template>

<script>
import Pokemon from './Pokemon'

import axios from 'axios'

export default {
  name: 'Application',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
    .then((response) => {
      this.pokemons = response.data.results
      this.filteredPokemons = response.data.results
    })
    .catch((error) => {
      console.log(error.message);
    })
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons
      if(this.busca.trim().length == 0){
        this.filteredPokemons = this.pokemons
      }
      else{
        this.filteredPokemons = this.pokemons.filter((pokemon) => pokemon.name == this.busca)
      }
    }
  },
  computed: {
  },
  components: {
    Pokemon
  }
}
</script>

<style scoped>
  #buscarBtn{
    margin-top: 2%;
  }
  #buscarBtn:hover{
    background-color: #1f7fbe;
  }
</style>
