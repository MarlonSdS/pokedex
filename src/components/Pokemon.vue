<template>
  <div>
      <h1>{{num}} {{nameUpper}}</h1>
      <small>{{url}}</small>
  </div>
</template>

<script>
import axios from 'axios'
export default {

    created: function(){
        axios.get(this.url).then(res =>{
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            console.log(this.pokemon.type)
            console.log(this.pokemon.front)
        })
    },

    data(){
        return{
           pokemon: {} 
        }
        
    },

    props: {
        name: String,
        url: String,
        num: Number
    },
    computed:{
        nameUpper(){
            //var newName = name[0].toUpperCase() + name.slice(1);
            return this.name[0].toUpperCase() + this.name.slice(1);
        }
    }

}
</script>

<style>

</style>