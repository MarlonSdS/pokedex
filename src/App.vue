<template>
<div id="app">
  <img src="./assets/pokedex.png" class="logo">
  
  <div class="capa">
    <div class="bord-1 column is-half is-offset-one-quarter">
      <div class="busca">
        <input type="text" class="input is-rounded" id="" placeholder="Buscar pokémon pelo nome" v-model="busca">
        
      </div>
      
      <div >
            <div v-for="(poke) in resultadoBusca" :key="poke.url">
              <pokemon :name="poke.name" :url="poke.url" :num="poke.num"/>
            </div>
        </div>
    </div>
  
    
  </div>
  
</div>
</template>

<script>
import axios from 'axios';
import pokemon from './components/Pokemon.vue';

export default {
  name: 'App',

  data(){
    return{
      pokemons: [],
      busca: ''
    }
  },

  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res =>{
      console.log(res.data.results);
      this.pokemons = res.data.results;
    }).catch(err =>{
      console.log(err);
    })
  },
  components: {
    pokemon
  },
  computed: {
    resultadoBusca: function(){
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name.includes(this.busca))
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.logo{
  height: 100px;
  margin-bottom: 5%;
}

.busca{
  display: flex;
  flex-direction: row;
}

.capa{
  background-color: red;
}

.bord-1{
        background-color: grey;
    }
</style>
