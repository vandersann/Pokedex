<template>
  <v-app>
    <v-card>
      <v-container>
        {{pokemon}}
      </v-container>
    </v-card>
  </v-app>
</template>

<script>
import axios from "axios";


export default {
  name: 'App',

  components: {},

  data() {
    return {
      pokemons: []
      }
    },

  mounted (){
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=493")
      .then((response) => {
        this.pokemons = response.data.results;
      });
  },
};

</script>
<style>
#app{
  background: linear-gradient(
      to bottom right,
      #F3DAED,
      #B7A3E0
    )
    no-repeat center center fixed !important;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover !important;
    background-position: center;
    min-height: 100vh;
}
</style>