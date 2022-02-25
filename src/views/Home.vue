<template>
  <div class="Home">
    <img alt="pokewiky" src="../assets/pokewiky.png">
    <div class="center">
      <input type="text" v-model="idPokemon">
      <button type="button" @click="buscar">Buscar</button>
      <img :src="imagen" alt="">
      <MostrarPokemon/>
   
    </div>
  </div>
</template>

<script>
import axios from "axios";
import MostrarPokemon from "@/components/MostrarPokemon.vue";

export default{
  components:{
    MostrarPokemon
  },
  data(){
    return{
      show: false,
      isActive: true,
      imagen: "",
      idPokemon:""
    };
  },
  methods:{
    buscar(){
      axios
        .get(`https://pokeapi.co/api/v2/pokemon/${this.idPokemon}`)
        .then((response) =>{
        console.log(response.data.sprites.front_default);
        this.imagen=response.data.sprites.front_default;
        //console.log(response);
    })
    .catch((err)=>{
      console.log(err);
    });
    }
  }
}
</script>

<style scoped>
img{
    width:35%;
    height:35%;
  }
</style>
