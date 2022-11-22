<template>
  <v-app>
    <v-container fluid>
      <v-container>
        <v-row class="d-flex justify-space-between">
          <v-col cols="12">
            <v-img
              :src="require('../src/assets/title50.png')"
              class="mx-auto"
              :aspect-ratio="16 / 9"
              width="500"
            />
          </v-col>
          <v-col cols="12">
            <h1 class="text-center white--text mb-6">
              by
              <a
                class="black--text"
                href="https://github.com/vandersann"
                target="_blank"
                >Vandersann💡</a
              >
            </h1>
          </v-col>
        </v-row>

        <v-text-field
          v-model="search"
          label="Search for"
          placeholder="type here..."
          @click="resetInput"
          clearable
          solo
          dense
          prepend-inner-icon="mdi-magnify"
        ></v-text-field>
        <v-row>
          <v-col
            cols="6"
            md="2"
            v-for="pokemon in filtered_pokemons"
            :key="pokemon.name"
          >
            <PokemonCard
              :pokemon="pokemon"
              @clicked="show_pokemon"
              class="d-flex"
            />
          </v-col>
        </v-row>
      </v-container>
    </v-container>

    <PokemonInfoDialog
      :show.sync="show_dialog"
      :selected_pokemon="selected_pokemon"
    />

    <audio autoplay="autoplay" controls="controls" loop="true">
      <source src="./assets/audio/pokemonTema.mp3" type="audio/mp3" />
    </audio>
  </v-app>
</template>

<script>
import axios from "axios";

import PokemonCard from "./components/PokemonCard.vue";
import PokemonInfoDialog from "./components/PokemonInfoDialog.vue";

import confirmaAudio from "./assets/audio/confirma.wav";
export default {
  name: "App",

  components: {
    PokemonCard,
    PokemonInfoDialog,
  },

  data() {
    return {
      pokemons: [],
      search: "",
      show_dialog: false,
      selected_pokemon: null,
    };
  },

  mounted() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=1000")
      .then((response) => {
        this.pokemons = response.data.results;
      });
  },
  methods: {
    show_pokemon(id) {
      axios.get(`https://pokeapi.co/api/v2/pokemon/${id}`).then((response) => {
        this.selected_pokemon = response.data;
        this.show_dialog = !this.show_dialog;
      });
    },

    get_move_level(move) {
      for (let version of move.version_group_details) {
        if (
          version.version_group.name == "scarlet-violet" &&
          version.move_learn_method.name == "level-up"
        ) {
          return version.level_learned_at;
        }
      }
      return 0;
    },

    play_audio(soundFile) {
      if (soundFile) {
        let audio = new Audio(soundFile);
        audio.play();
      }
    },

    clickMouse: function () {
      this.play_audio(confirmaAudio);
    },

    resetInput() {
      this.search = "";
      this.selected_pokemon = null;
    },
  },
  computed: {
    filtered_pokemons() {
      return this.pokemons.filter((item) => {
        return item.name.includes(this.search);
      });
    },
  },
};
</script>

<style>
#app {
  width: 100vw;
  background: linear-gradient(to left, #ee7752, #e73c7e, #23a6d5, #23d5ab);
  background-size: 300% 300%;
  animation: colors 10s ease infinite;
}

@keyframes colors {
  0% {
    background-position: 0% 50%;
  }

  50% {
    background-position: 100% 50%;
  }

  100% {
    background-position: 0% 50%;
  }
}

::-webkit-scrollbar {
  width: 15px;
}

::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0);
}

::-webkit-scrollbar-thumb {
  background: linear-gradient(
    transparent,
  black
  );
  border-radius: 10px;
}

.container {
  font-family: "Press Start 2P", cursive;
  font-size: 0.8em;
}

audio {
  position: absolute;
  filter: sepia(20%) saturate(70%) grayscale(1) contrast(99%) invert(12%);
  width: 250px;
  height: 25px;
  opacity: 0.7;
}

@media screen and (max-width: 342px) {
  h1 {
    font-size: 1em;
  }

  .v-text-field {
    font-size: 1em;
  }

  .v-text-field label {
    font-size: 0.8em;
  }

  audio {
    position: absolute;
    text-align: center;
    opacity: 0.5;
  }
}
</style>