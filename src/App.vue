<template>
  <v-app>
    <v-container>
      <v-container>
        <v-text-field
          v-model="search"
          label="Encontre aqui"
          placeholder="Digite... "
          solo
        ></v-text-field>
        {{ search }}
        <v-row>
          <v-col
            cols="2"
            v-for="pokemon in filtered_pokemons"
            :key="pokemon.name"
          >
            <v-card class="rounded-xl">
              <v-container>
                <v-row class="mx-0 d-flex justify-center">
                  <img
                    :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_id(
                      pokemon
                    )}.png`"
                    :alt="pokemon.name"
                    loading="lazy"
                    width="80%"
                  />
                </v-row>
                <h2 class="text-center">{{ get_name(pokemon) }}</h2>
              </v-container>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-container>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  name: "App",

  components: {},

  data() {
    return {
      pokemons: [],
      search: "",
    };
  },

  mounted() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=1100")
      .then((response) => {
        this.pokemons = response.data.results;
      });
  },
  methods: {
    get_id(pokemon) {
      return Number(pokemon.url.split("/")[6]);
    },
    get_name(pokemon) {
      return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1);
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
  background: linear-gradient(to bottom right, #f3daed, #b7a3e0) no-repeat
    center center fixed !important;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover !important;
  background-position: center;
  min-height: 100vh;
}
</style>