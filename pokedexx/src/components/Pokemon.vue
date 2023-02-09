<script>
import axios from 'axios'
export default {
    created: function () {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            this.currentImg = this.pokemon.front
        })
    },
    data() {
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
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
                    <small>Tipo: {{ pokemon.type }}</small>
                </div>
            </div>
            <div class="content">
                <button class="button is-primary is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
            </div>
        </div>
    </div>
</template>

<style>
.card{
    min-width: 250px;
    min-height: 350px;
    margin: 5px;
    background-color: #000227 !important;
    color: #fff !important;
}

img{
    max-width: 150px !important;
    margin: auto;
    padding-top: 50px;
}
</style>