<template>
  <div id="pokemon">
    <div class="card">
        <div class="card-image">
            <figure>
            <img :src="currentImage" :alt="pokemon.name" @mouseover="currentImage = pokemon.back" @mouseleave="currentImage = pokemon.front">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-content">
                    <p class="title is-4">{{num}} - {{name | upper}}</p>
                    <p class="subtitle is-6">{{pokemon.type}}</p>
                </div>
            </div>

            <div class="content"></div>
        </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';

export default {
    created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            this.currentImage = this.pokemon.front
        })
    },
    data(){
        return{
            currentImage: '',
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },
    props:{
        num: Number,
        name: String,
        url: String
    },
    filters: {
        upper: function(value){
            var newName = value[0].toUpperCase() + value.slice(1)
            return newName 
        }
    }
}
</script>

<style>
    #pokemon{
        margin-bottom: 20px;
    }
</style>