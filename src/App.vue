<template>
  <div id="app">
    <img src="./assets/logo.png">
    <div class = "column is-half is-offset-one-quarter"> 
      <hr>
      <p class="title is-4">Pokedéx</p> 
      <hr>
      <input class="input is-rounded" type="text" placeholder="Buscar Pokemon" v-model = "busca">
       <button @click = "buscar" class="button is-primary" id = "buscaBtn">Buscar</button>
      <hr>
      <br>
    <div v-for = "(poke, index) in filteredPokemons" :key = "poke.url">
     <pokemons :name = "poke.name" :url = "poke.url" :num = "index +1"/> 
     </div>
    </div>

    
  </div>
</template>

<script>
import axios from 'axios'
import pokemons from "./components/pokemon"
export default {
  name: 'App',
  data(){
    return {
      busca: '',
      pokemons : [],
      filteredPokemons: []
  }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then((res) => {
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    }).catch((erro) => {
      console.log(erro)
    })
  },
  components: {
    pokemons
  },
  methods: {
    buscar: function(){      
      if(this.busca == '' | this.busca == ' ' ){
      this.filteredPokemons = this.pokemons;
      }else{
      this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }    
    }
  },
  computed: {
    
  }
}
</script>

<style>
#buscaBtn{
  margin: 2% auto auto 10px ;
}
</style>
