<template>
  <div class="Home">
    <img alt="pokewiky" src="../assets/pokewiky.png">
    <div class="center">
       <b-nav-form class="col-md-6 offset-md-3">
          <b-form-input size="sm" class="mr-sm-2" placeholder="Busca tu Pokémon..." type="text" v-model="idPokemon">
          </b-form-input>
          <b-button variant="danger" size="sm" type="button" @click="buscar">Buscar</b-button>
        </b-nav-form>
         <b-card title="Pokemón" img-top tag="article" style="max-width: 25rem;" class="col-md-8 offset-md-4">
              <title>{{name}}</title>
              <img :src="imagen" @click="imagen" alt="">
        <b-card-text>
             Aquí aparecera la información completa de tu Pokémon
      </b-card-text>
    <b-button href="#" variant="warning">Agregar a favoritos </b-button>
     
  </b-card>
   <img src= "../assets/pikachu.gif" width="2px" height="2px" alt="">
      <!---->
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
      idPokemon:"",
      name:""
    };
  },
  methods:{
    buscar(){
      axios
        .get(`https://pokeapi.co/api/v2/pokemon/${this.idPokemon}`)
        .then((response) =>{
        console.log(response.data.sprites.front_default);
        this.imagen=response.data.sprites.front_default;
        this.name=response.data.name
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
    width:25%;
    height:25%;
  }
</style>
