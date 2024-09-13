<script>
import SearchCustom from './components/SearchCustom.vue';
export default{
  components: {
    SearchCustom,
  },
  data(){
    return{
      pokemonInfo : null
    }
  },
  methods: {
    handlePokemonInfo(data){
      this.pokemonInfo = data;
    }
  }
}
</script>

<template>
   <h1>App.vue... https://pokeapi.co/api/v2/pokemon/{id or name}/</h1>
   <div class="container" style="width: 100%;">
      <div class="ms_pokedex" style="margin: 0 auto; background-color: aliceblue; width: 75%; height: 700px; display: flex;">
        <div class="ms_pokedex-l" style="width: 50%; background-color: darkred; color: white; display: flex; flex-direction: column;">
          <SearchCustom @pokemon-info="handlePokemonInfo "/> 
          <div class="ms_poke-image" style="width: 225px; height: 225px;">
            <img :src="pokemonInfo.sprites.front_default" alt="Immagine Pokemon" style="width: 100%;" v-if="pokemonInfo">
            <img src="../src/assets/pixel-pokeball-pixel-art-pokemon-pokeball-nintendo-8bit_grande.webp" alt="Placeholder Image" style="width: 100%;" v-else>
          </div> <br>
          Informazioni Pokémon <br>
        </div>
        <div class="ms_pokedex-r" style="width: 50%; background-color: brown; color: white;">
          La mia Squadra Pokémon, salvata in localStorage
        </div>
    </div>
   </div>
   
</template>

<style>

</style>
