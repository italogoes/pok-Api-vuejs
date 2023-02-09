<script setup>
  import axios from 'axios'
  import Pokemon from './components/Pokemon.vue'
</script>

<script>
  export default {
    name: 'App',
    data(){
      pokemons: []
      busca: ''
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
  <div id="ap">
    <h2 class="logo">Lista de Pokemons</h2>
    <input class="input is-rounded" type="text" placeholder="Buscar pokemon pelo nome" v-model="busca">
    <button class="button btn-pesquisa is-primary is-fullwidth" @click="mudarSprite">Buscar</button>
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

input[type=text]{
  background-color: #3e3e3e;
  color: #fff;
  margin-bottom: 10px;
  border: 1px solid rgb(33, 33, 144);
}

.btn-pesquisa{
  margin-bottom: 50px;
  border-radius: 20px !important;
}

input[type=text]::placeholder{
  color: #a1a1a1;
}

.flex{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
</style>
