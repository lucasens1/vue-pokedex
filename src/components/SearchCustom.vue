<script>
export default {
  data() {
    return {
      pokeName: "",
      errorMessage: null
    };
  },
  methods: {
    async getPokemon() {
      try {
        const response = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${this.pokeName}/`
        );
        if (!response.ok) {
          throw new Error("Pokemon non trovato");
        }

        const data = await response.json();
        this.$emit('pokemon-info', data);
        console.log(this.pokemonInfo);
      } catch (error) {
        this.pokemonInfo = null;
        this.errorMessage = error.message;
      }
    },
  },
};
</script>

<template>
  <div class="ms_search">
    <input type="text" name="poke-name" v-model="pokeName" />
    <button @click="getPokemon">Cerca Pokemon</button>

    <p v-if="errorMessage">{{ errorMessage }}</p>
  </div>
</template>

<style></style>
