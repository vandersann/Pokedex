<template>
  <v-card @click="show_pokemon(get_id(pokemon))" :flat="flat" color="rgba(248,248,255, 0.6)">
    <v-container>
      <h3 class="align-start mb-1 mt-1">No. {{ get_id(pokemon) }}</h3>
      <v-row class="mx-0 d-flex justify-center">
        <img
          :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_id(
            pokemon
          )}.png`"
          :alt="pokemon.name"
          width="80%"
        />
      </v-row>
      <h2 class="text-center">{{ get_name(pokemon) }}</h2>
    </v-container>
  </v-card>
</template>

<script>
export default {
  props: {
    pokemon: Object,
    flat: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    get_id(pokemon) {
      return Number(pokemon.url.split("/")[6]);
    },
    get_name(pokemon) {
      return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1);
    },
    show_pokemon(id) {
      this.$emit("clicked", id);
    },
  },
};
</script>

<style lang="scss" scoped></style>
