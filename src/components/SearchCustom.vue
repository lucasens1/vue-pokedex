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
          `https://pokeapi.co/api/v2/pokemon/${this.pokeName.toLowerCase()}/`
        );
        if (!response.ok) {
          throw new Error("Pokemon non trovato");
        }

        const data = await response.json();
        this.$emit('pokemon-info', data);
        this.errorMessage = null;
      } catch (error) {
        this.errorMessage = error.message;
      }
    },
  },
};
</script>

<template>
  <div class="ms_search">
    <input type="text" name="poke-name" v-model="pokeName" />
    <button @click="getPokemon" style="display: flex; align-items: center; gap: 6px;">Cerca <img src="https://cdn3.emoji.gg/emojis/pokeball.png" width="20px" alt="pokeball"></button>

    <p v-if="errorMessage">{{ errorMessage }}</p>
  </div>
</template>

<style>
/* Stile Searchbar */
.ms_search{
  padding: 12px 8px;
  display: flex;
  justify-content: space-evenly;
  width: 100%;
}

.ms_search > input,
.ms_search > button {
  padding: 12px;
  border-radius: 20px;
  transition: 0.7s;
  border: none;
}

.ms_search > input {
  width: 55%;
}

.ms_search > input:focus{
  border: none;
  outline: none;
  background-color: rgba(0, 0, 0, 0.2);
  transition: 0.7s all;
  color: white;
}

.ms_search > input:hover{
  border: none;
  outline: none;
  background-color: rgba(0, 0, 0, 0.2);
  transition: 0.7s all;
  color: white;
}

.ms_search > button:hover{
  border: none;
  outline: none;
  background-color: rgba(0, 0, 0, 0.2);
  transition: 0.7s all;
  color: white;
}
</style>
