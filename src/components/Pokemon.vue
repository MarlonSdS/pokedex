<template>
  <div>
    <div class="card">
        <div class="card-image">
            <figure >
            <img :src="this.currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-left">
                
            </div>
            <div class="media-content">
                <p class="title is-4">{{pokemon.num}} {{nameUpper}}</p>
                <p class="subtitle is-6">{{pokemon.type}}</p>
            </div>
            </div>

            <div class="content">
                <button class="button is-normal" @click="mudarSprite">Mudar Sprite</button>
            </div>
        </div>
    </div>

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
            this.currentImg = res.data.sprites.front_default;
            this.pokemon.num = res.data.game_indices[3].game_index;
            console.log(this.pokemon.num)
            console.log(this.pokemon.back)
        })
    },

    data(){
        return{
            isFront: true,
            currentImg: '',
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
    },
    methods: {
        mudarSprite: function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }else{
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
    
</script>

<style>
    .card{
        margin-top: 1%;
        background-color: rgb(160, 241, 255) !important;
    }

    
</style>