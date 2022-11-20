<template>
  <v-card
    @mouseenter="slideMouse"
    class="card rounded-lg"
    @click="show_pokemon(get_id(pokemon))"
    outlined
    elevation="2"
    color="rgba(280,280,280, 0.80)"
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
          width="70%"
        />
      </v-row>
      <h3 class="card-title">
        {{ get_name(pokemon) }}
      </h3>
    </v-container>
  </v-card>
</template>

<script>
import selecaoAudio from "../assets/audio/selecao.mp3";
import confirmaAudio from "../assets/audio/confirma.wav";

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
      this.play_audio(confirmaAudio);
    },

    play_audio(soundFile) {
      if (soundFile) {
        let audio = new Audio(soundFile);
        audio.play();
      }
    },

    slideMouse: function () {
      this.play_audio(selecaoAudio);
    },
  },
};
</script>

<style>
.card {
  font-size: 1.8em;
  width: 80%;
  box-shadow: 0 0 5px 0px #e2e2e2;
  position: relative;
  cursor: pointer;
}

.card:after,
.card:before {
  content: "";
  position: absolute;
  bottom: 0;
  top: 0;
  left: 0;
  right: 0;
  transition: transform 0.1s ease-in-out;
}

.card:after {
  border: 3px solid rgb(84, 82, 82);
  border-radius: 8px;
  transform: scaleZ(0);
  animation: btn-pisca 0.5s linear infinite;
}

.card:hover:after {
  transform: scaleX(1);
}

@keyframes btn-pisca {
  0% {
    opacity: 0;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    opacity: 1;
  }
}

.card-title {
  background-size: flex;
  color: black;
  position: center;
  text-align: center;
  margin-top: 15px;
  font-size: 1em;
}
.card-number {
  background-size: flex;
  color: black;
  position: left;
  text-align: start;
  margin-bottom: 15px;
}

/* Media Screen */

@media screen and (max-width: 1903px) {
  .card {
    font-size: 1.3em;
  }
}

@media screen and (max-width: 1263px) {
  .card {
    font-size: 0.8em;
  }
}

@media screen and (max-width: 959px) {
  .card {
    font-size: 1.8em;
  }
}

@media screen and (max-width: 418px) {
  .card {
    font-size: 1.3em;
  }
}

@media screen and (max-width: 384px) {
  .card {
    font-size: 1.2em;
  }
}

@media screen and (max-width: 353px) {
  .card {
    font-size: 1em;
  }
}

@media screen and (max-width: 320px) {
  .card {
    font-size: 0.8em;
  }
}

@media screen and (max-width: 271px) {
  .card {
    font-size: 0.6em;
  }
}
</style>
