<script setup>
  import axios from 'axios'
  import Pokemon from './components/Pokemon.vue'
</script>

<script>
  export default {
    name: 'App',
    data () {
      return {
        pokemons: [],
        PokemonsFiltrados: [],
        busca: ''
      }
    },
    created: function(){
      axios.get('https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0').then(res => {
        this.pokemons = res.data.results
        this.PokemonsFiltrados = res.data.results
      })
    },
    components: {
      Pokemon
    },
    methods: {
      buscar: function(){
        this.PokemonsFiltrados = this.pokemons // resetando o array de pokemons
        if(this.busca == '' || this.busca == ' '){
          // se for vazio retorne os pokemons
          this.PokemonsFiltrados = this.pokemons
        } else {
          // se o usuario digitou algo então vou filtrar pela letra ou palavra digitada
          this.PokemonsFiltrados = this.pokemons.filter((pokemon) => pokemon.name.toLowerCase().includes(this.busca.toLowerCase()))
          console.log(this.busca)
        }
      }
    }
  }
</script>

<template>
  <div id="app">
    <h2 class="logo">Lista de Pokemons</h2>
    <input 
    type="text" 
    placeholder="Buscar pokemon pelo nome" 
    v-model="busca" class="input is-rounded"
    >
    <button class="button btn-pesquisa is-primary is-fullwidth" @click="buscar">Buscar</button>

    <div class="flex is-half is-offset-one-quarter">
      <div v-for="(poke, index) in PokemonsFiltrados" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
  </div>
</template>

<style>
html,body{
  height: 100%;
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
  gap: 20px;
}
</style>
