<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="currentImg" alt="Placeholder image">
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{num}} - {{name | upperFirstLetter}}</p>
            <p class="subtitle is-6">type: {{pokemon.type}}</p>
          </div>
        </div>

        <div class="content">
          <button class="button is-medium is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
        </div>
      </div>
    </div>
  </div>
  
</template>

<script>
import axios from 'axios'

export default {
  name: 'Pokemon',
  created: function(){
    axios.get(this.url)
    .then((response) => {
      this.pokemon.type = response.data.types[0].type.name
      this.pokemon.sprites = {front: response.data.sprites.front_default, back: response.data.sprites.back_default}
      this.currentImg = this.pokemon.sprites.front
    })
    .catch((error) => {
      console.log(error);
    })
  },
  data(){
    return {
      isFront: true,
      currentImg: '',
      pokemon: {
        type: "",
        sprites: {
          front: "",
          back: ""
        }
      }
    }
  },
  props: {
    num:Number,
    name:String,
    url:String
  },
  filters: {
    upperFirstLetter: function(value){
      let new_value = value[0].toUpperCase() + value.slice(1)
      return new_value
    }
  },
  methods: {
    mudarSprite: function(){
      if(this.isFront){
        this.isFront = false
        this.currentImg = this.pokemon.sprites.back
      }
      else{
        this.isFront = true
        this.currentImg = this.pokemon.sprites.front
      }
    }
  }
}
</script>

<style scoped>
  #pokemon{
    margin-top: 2%;
    text-align: center;
  }

</style>
