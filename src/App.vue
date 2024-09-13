<script>
import SearchCustom from "./components/SearchCustom.vue";
export default {
  components: {
    SearchCustom,
  },
  data() {
    return {
      pokemonInfo: null,
      currentSprite: null,
      intervalId: null,
      team: []
    };
  },
  created() {
    // Carica la squadra dal LocalStorage quando il componente è creato
    this.team = JSON.parse(localStorage.getItem('pokemonTeam')) || [];
  },
  computed: {},
  methods: {
    handlePokemonInfo(data) {
      this.pokemonInfo = data;
      console.log(this.pokemonInfo);
      this.handlePokemonImage();
    },
    handlePokemonImage() {
      if (this.intervalId) {
        clearInterval(this.intervalId);
      }

      this.currentSprite = this.pokemonInfo.sprites.front_default;

      this.intervalId = setInterval(() => {
        if (this.currentSprite === this.pokemonInfo.sprites.front_default) {
          this.currentSprite = this.pokemonInfo.sprites.back_default;
        } else {
          this.currentSprite = this.pokemonInfo.sprites.front_default;
        }
      }, 1500);
    },
    statBar(statVal) {
      const maxStat = 100;
      return (statVal / maxStat) * 100 + "%";
    },
    firstL(word) {
      return word.charAt(0).toUpperCase() + word.slice(1).toLowerCase();
    },
    addToTeam() {
      if (!this.pokemonInfo) {
        console.error("Nessun Pokémon selezionato");
        return;
      }

      // Aggiungi il Pokémon alla squadra locale
      this.team.push(this.pokemonInfo);

      // Salva la squadra aggiornata nel LocalStorage
      localStorage.setItem("pokemonTeam", JSON.stringify(this.team));

      console.log("Pokémon aggiunto alla squadra");
    },
  },
  beforeDestroy() {
    if (this.intervalId) {
      clearInterval(this.intervalId);
    }
  },
};
</script>

<template>
  <div class="container">
    <div class="ms_pokedex">
      <div class="ms_pokedex-l">
        <SearchCustom @pokemon-info="handlePokemonInfo" />

        <div class="ms_poke-image">
          <div class="ms_poke-image-rel">
            <img
              :src="currentSprite"
              alt="Immagine Pokemon"
              v-if="pokemonInfo"
            />
            <img
              src="../src/assets/pixel-pokeball-pixel-art-pokemon-pokeball-nintendo-8bit_grande.webp"
              alt="Placeholder Image"
              v-else
            />
          </div>
        </div>

        <div v-if="pokemonInfo" class="ms_poke-card">
          <h3 class="ms_text-center">{{ firstL(pokemonInfo.name) }}</h3>
          <div v-for="pokeStat in pokemonInfo.stats" class="battle-stats">
            <p>
              <strong>{{ firstL(pokeStat.stat.name) }}</strong> :
              {{ pokeStat.base_stat }}
            </p>
            <div class="stat-bar">
              <div
                class="stat-bar-fill"
                :style="{ width: statBar(pokeStat.base_stat) }"
              ></div>
            </div>
          </div>
          <p class="ms_text-center ms_btn" @click="addToTeam">Aggiungi Pokemon</p>
        </div>
        <div v-else>
          <p class="pt-24">
            Inserisci un nome Pokémon per vedere le informazioni.
          </p>
        </div>
      </div>

      <div class="ms_pokedex-r">
        <div v-if="team.length">
          <h3 class="ms_text-center">La mia Squadra Pokémon</h3>
          <div class="ms_d-flex" v-for="pokemon in team" :key="pokemon.id">
            <p>{{ firstL(pokemon.name) }}</p>
            <img
              :src="pokemon.sprites.front_default"
              alt="Immagine Pokémon"
              style="width: 110px"
            />
          </div>
        </div>
        <div v-else>
          Aggiungi un Pokémon al tuo team!
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.ms_d-flex{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.ms_btn {
  margin-top: 12px;
  padding: 12px;
  background-color: rgba(49, 45, 45, 0.709);
  border-radius: 24px;
  cursor: pointer;
}
.pt-24 {
  padding: 24px 24px;
}
.ms_text-center {
  text-align: center;
}
.ms_poke-card {
  margin: 16px;
  border-radius: 16px;
  padding: 16px;
  background-color: #ccbebe7d;
}

.battle-stats > p {
  padding-top: 12px;
}
/* Contenitore della barra */
.stat-bar {
  width: 100%;
  background-color: white;
  border-radius: 12px;
  overflow: hidden;
  height: 20px;
  transition: 0.7s all;
}

/* Parte riempita della barra */
.stat-bar-fill {
  height: 100%;
  background-color: #4caf50;
  width: 0;
  transition: width 0.5s ease;
}

.ms_poke-image {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: white;
}

.ms_poke-image-rel {
  width: 100%; /* Imposta la larghezza del contenitore interno */
  height: 160px; /* Limita l'altezza massima */
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden; /* Nasconde le parti dell'immagine che escono dai bordi */
}

.pokemon-img,
.placeholder-img {
  width: 100%; /* Adatta l'immagine alla larghezza del contenitore */
  height: 160px; /* Mantiene il rapporto di aspetto dell'immagine */
}

.container {
  width: 100%;
  margin-top: 120px;
}

.ms_pokedex {
  margin: 0 auto;
  border: 10px solid black;
  border-radius: 24px;
  width: 80%;
  min-height: 700px;
  display: flex;
}

.ms_pokedex-l {
  width: 50%;
  background-color: darkred;
  color: white;
  display: flex;
  flex-direction: column;
  border-top-left-radius: 12px;
  border-bottom-left-radius: 12px;
}

.ms_pokedex-r {
  padding: 20px;
  width: 50%;
  background-color: brown;
  color: white;
  border-top-right-radius: 12px;
  border-bottom-right-radius: 12px;
}
</style>
