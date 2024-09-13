<script>
import SearchCustom from './components/SearchCustom.vue';
export default{
  components: {
    SearchCustom,
  },
  data(){

  },
  methods: {
    
  }
}
</script>

<template>
   <h1>App.vue... https://pokeapi.co/api/v2/pokemon/{id or name}/</h1>
   <div class="container" style="width: 100%;">
      <div class="ms_pokedex" style="margin: 0 auto; background-color: aliceblue; width: 60%; height: 700px; display: flex;">
        <div class="ms_pokedex-l" style="width: 50%; background-color: darkred; color: white; display: flex;">
          <SearchCustom /> <br> 
          Immagine Pokémon <br>
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
