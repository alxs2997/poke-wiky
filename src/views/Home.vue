<template>
  <div class="Home">
    <img alt="pokewiky" width="300" src="../assets/pokewiky.png">
     <div class="center">
       <b-nav-form class="col-md-6 offset-md-3">
          <b-form-input size="sm" class="mr-sm-2" placeholder="Busca tu Pokémon..." type="text" v-model="idPokemon">
          </b-form-input>
          <b-button variant="danger" size="sm" type="button" @click="buscar">Buscar</b-button>
        </b-nav-form>
    <b-card
          :title="nombrePokemon"
          :img-src="imagenPokemon"
          :sub-title="genera"
          img-alt="Image"
          img-top
          tag="article"
          :style="{maxWidth:'20rem',borderStyle:'solid',borderColor:colorPokemon, marginTop:'15px'}"
        class="col-6 offset-3"
        >
          <b-card-text>
          {{descPokemon}}
          </b-card-text>
          <b-card-text>
            <strong>Peso: </strong>{{pesoPokemon}} kg. <br>
            <strong>Altura: </strong>{{alturaPokemon}} ft<br>
            <strong>Tipos: </strong>{{tipo.toString()}} <br>
            <strong>Generación: </strong>{{queGeneracion}}
          </b-card-text>

          <b-button href="#" variant="danger">{{this.mensajeError}}</b-button>
      </b-card>
    </div>
  </div>
</template>

<script>
import axios from "axios";
//import MostrarPokemon from "@/components/MostrarPokemon.vue";

export default{
  components:{
    //MostrarPokemon
  },
  data(){
    return{
      mensajeError:"",
      imagenPokemon: "",
      idPokemon:"",
      nombrePokemon:"",
      descPokemon:"",
      radioGenero:0,
      genera:"",
      pesoPokemon: 0,
      alturaPokemon: 0,
      tipo:[],
      evolucion:"",
      colorPokemon:"",
      queGeneracion:""
    };
  },
  methods:{
    limpiarPokemon(){
      this.tipo = []
      this.mensajeError=""
    },
    async buscar(){
      let searchUrl = `https://pokeapi.co/api/v2/pokemon/${this.idPokemon}`
      try {
        const pokeData = await axios.get(searchUrl)
        console.log(pokeData)
        const speciesUrl = pokeData.data.species.url
        const speciesData = await axios.get(speciesUrl)
        this.procesarPokemon(pokeData.data, speciesData.data)
      }catch(error){
        console.log(error)
        this.mensajeError=error.message

      }

    },
    async procesarPokemon(poke, species){
      this.limpiarPokemon()
      console.log("Entering procesar Pokemon")
      console.log(poke)
      console.log(species)
      //this.idPokemon = poke.id
      this.nombrePokemon = poke.name
      // Buscar descripción
      for(let desc of species.flavor_text_entries){
        if(desc.language.name==="es"){
          console.log("We found spanish description!")
          this.descPokemon = desc.flavor_text
          break
        }
      }
      this.imagenPokemon = poke.sprites.other["official-artwork"].front_default
      console.log(this.imagenPokemon)
      this.pesoPokemon = poke.weight
      this.alturaPokemon = poke.height


      for(let tipo of poke.types){
        //this.tipo.push(type.type.name)
        const datosTipo = await axios.get(tipo.type.url)
        for(let tipo of datosTipo.data.names){
          if(tipo.language.name==="es"){
            this.tipo.push(tipo.name)
            break
          }
        }

      }
      this.radioGenero = species.gender_rate
      for(let gen of species.genera){
        if(gen.language.name==="es"){
          this.genera=gen.genus
          break
        }
      }
      this.queGeneracion = species.generation.name
      this.colorPokemon = species.color.name
    }
  }
}
</script>

<style scoped>
</style>
