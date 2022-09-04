<template>
  <h1 v-if="!pokemon">Loading...</h1>

  <div v-else>
    <h1>Who is this pokemon?</h1>
    <PokemonPicture :pokemon-id="pokemon.id" :show-pokemon="showPokemon" />
    <PokemonOptions :pokemons="pokeArr" @selection="checkAnswer" />

    <template v-if="showAnswer">
      <h2 class="fade-in">{{ message }}</h2>
      <button @click="newGame">New Game</button>
    </template>
  </div>
</template>

<script>
import PokemonOptions from '../components/PokemonOptions.vue';
import PokemonPicture from '../components/PokemonPicture.vue';

import getPokemonOptions from '../helper/getPokemonOptions.js';

export default {
  components: { PokemonOptions, PokemonPicture },

  data() {
    return {
      pokeArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: '',
    };
  },

  methods: {
    async mixPokeArr() {
      this.pokeArr = await getPokemonOptions();
      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokeArr[rndInt];
    },

    checkAnswer(pokeId) {
      this.showPokemon = true;
      this.showAnswer = true;

      if (pokeId === this.pokemon.id) {
        this.message = `Correct!!!! is, ${this.pokemon.name}`;
      } else {
        this.message = `Sorry is ${this.pokemon.name}`;
      }
    },

    newGame() {
      this.pokeArr = [];
      this.showAnswer = false;
      this.showPokemon = false;
      this.pokemon = null;
      this.mixPokeArr();
    },
  },

  mounted() {
    this.mixPokeArr();
  },
};
</script>
