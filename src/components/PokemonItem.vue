<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
        <figure>
          <img
            :src="currentImage"
            alt="Placeholder image"
          />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">
              {{ index }} - {{ upperFirstCaracter(name) }}
            </p>
            <p class="subtitle is-6">Tipo: {{ pokemon.type }}</p>
          </div>          
        </div>
        <button class="button" @click="alterSprite" >Mudar Sprite</button> 
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  created: function () {
    axios.get(this.url).then((response) => {
      this.pokemon.type = response.data.types[0].type.name;
      this.pokemon.front = response.data.sprites.front_default;
      this.pokemon.back = response.data.sprites.back_default;
      this.currentImage =  this.pokemon.front;
      console.log(this.pokemon);
    });
  },
  data() {
    return {
      isFront: true,
      currentImage: "",
      pokemon: {
        type: "",
        front: "",
        back: "",
      },
    };
  },
  props: {
    index: Number,
    name: String,
    url: String,
  },
  methods: {
    upperFirstCaracter: function (value) {
      value = value.toString();
      return value.charAt(0).toUpperCase() + value.slice(1);
    },
    alterSprite: function(){
      if(this.isFront){
        this.currentImage = this.pokemon.back;
        this.isFront = false;
        return;
      }
     
     this.currentImage = this.pokemon.front;
     this.isFront = true;

    },
  },
};
</script>

<style>
  #pokemon{
    margin-top: 1%;
  }
</style>