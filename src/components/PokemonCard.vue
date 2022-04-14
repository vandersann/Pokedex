<template>
  <v-card
  class="card rounded-lg"
  @click="show_pokemon(get_id(pokemon))"
  :flat="flat"
  color="rgba(280,280,280, 0.45)"
  >
    <v-container>
      <h3 class="card-number">No. {{ get_id(pokemon) }}</h3>
      <v-row class="mx-0 d-flex justify-center">
        <img
          :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_id(
            pokemon
          )}.png`"
          loading="lazy"
          :alt="pokemon.name"
          mb-2
          width="80%"
        />
      </v-row>
      <h3
      class="card-title">
      {{ get_name(pokemon) }}
      </h3>
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

<style>
.card{
  width: 80%;
  background-size: flex;
  border-style: outset;
  position: relative;
  transform-style:preserve-3d;
  will-change: transform;
  transition: transform .5s;
}
.card:hover{
  transform: translateZ(10px)
  rotateX(20deg) rotateY(30deg);
}
.card-title{
  background-size: flex;
  font-color:black;
  position: center;
  text-align:center;
  margin-top:15px;
}
.card-number{
  background-size: flex;
  font-color:black;
  position: left;
  text-align:start;
  margin-bottom:15px;
}
</style>
