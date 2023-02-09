<script setup>
  import axios from 'axios'
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
    }
  }
</script>

<template>
  <header>

  </header>
</template>
