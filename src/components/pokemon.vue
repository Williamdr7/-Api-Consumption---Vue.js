<template>
<div class = "data">     

    <div class="card">
  <div class="card-image">
    <figure class = "figure">
      <img :src="this.currentImg" alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
     
      <div class="media-content">
        <p class="title is-4">{{name | upper}}</p>
        <p class="subtitle is-6">{{pokemon.type}}</p>
      </div>
    </div>
    <div class="content">
    </div>
  </div>
</div>
<button @click = "trocarImagem" class="button is-fullwidth">Trocar Imagem</button>

</div>
</template>

<script>
import axios from 'axios'
export default {
    created: function(){
        axios.get(this.url).then((data) => {
            this.pokemon.type = data.data.types[0].type.name;
            this.pokemon.front = data.data.sprites.front_default;
            this.pokemon.back = data.data.sprites.back_default;  
            this.currentImg = this.pokemon.front          
        })
    },
    data(){
        return { 
            isFront: true,
            btn: '',
            currentImg: '',
        pokemon: {
            type: "",
            front: "",
            back: ""
        }
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    filters: {
        upper: function(value){
            var nameUpper = value[0].toUpperCase() + value.slice(1)
            return nameUpper;
        }
    },
    methods: {
        trocarImagem: function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back
            }else{
                this.isFront = true;
                this.currentImg = this.pokemon.front
            }
        }
    }
}

</script>

<style scoped>
.data{
    width: 500px;
    height: auto;
    margin: 10px auto;
    border: 1px solid black;
}

</style>