<script>
import axios from 'axios'
export default {
    created: function () {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            this.currentImg = this.pokemon.front
            console.log(this.pokemon)
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
        </div>
    </div>
</template>

<style>
.card{
    min-width: 250px;
    min-height: 350px;
    margin: 5px;
    background-color: #000227;
    color: #fff;
}

img{
    max-width: 150px;
    margin: auto;
    padding-top: 50px;
}
</style>