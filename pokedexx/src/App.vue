<script setup>
  import axios from 'axios'
  import Pokemon from './components/Pokemon.vue'
</script>

<script>
  export default {
    name: 'App',
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
  <div id="app">
    <h2 class="logo">Lista de Pokemons</h2>
    <div class="flex is-half is-offset-one-quarter">
      <div v-for="(poke, index) in pokemons" :key="index">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
  </div>
</template>

<style>
body{
  background-color: #242424;
}

#app{
  max-width: 1400px;
  margin: auto;
}

.logo{
  font-size: 55px;
  text-align: center;
  padding: 30px 0;
  color: #fff;
}

.flex{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
</style>
