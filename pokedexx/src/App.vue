<script setup>
  import axios from 'axios'
  import Pokemon from './components/Pokemon.vue'
</script>

<script>
  export default {
    data(){
      pokemons: []
    },
    created: function(){
      axios.get('https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0').then(res => {
        console.log(res.data.results)
        this.pokemons = res.data.results
        console.log(this.pokemons)
      })
    },
    components: {
      Pokemon
    }
  }
</script>

<template>
  <div v-for="(poke, index) in pokemons" :key="index">
    <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
  </div>
</template>
