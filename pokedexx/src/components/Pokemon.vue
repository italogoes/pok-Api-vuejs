<script>
import axios from 'axios'
import '../assets/styles/index.sass'
export default {
    created: function () {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            this.currentImg = this.pokemon.front
            this.pokemon.abilities = res.data.abilities.map(ability => ability.ability.name)
        })
    },
    data() {
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                abilities: [],
                front: '',
                back: ''
            }
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    methods: {
        mudarSprite: function(){
            if(this.isFront){
                this.isFront = false
                this.currentImg = this.pokemon.back
            } else {
                this.isFront = true
                this.currentImg = this.pokemon.front
            }
        }
    }
}
</script>

<template>
    <div class="card">
        <div class="card-image">
            <figure class="image">
                <img :src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-content">
                    <h1>Pokemon: {{ num }} {{ name }}</h1>
                    
                </div>
            </div>
            <div class="content">
                <p><b> Tipo: {{ pokemon.type }}</b></p>
                <p><b>Habilidades:</b></p>
                <ul>
                    <li v-for="ability in pokemon.abilities">{{ ability }}</li>
                </ul>
                <button class="button is-primary is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
            </div>
        </div>
    </div>
</template>