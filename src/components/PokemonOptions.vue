<template>
  <div class="options-container">
    <ul>
      <li
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('selection', pokemon.id)"
      >
        {{ pokemon.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
}

li {
  background-color: #1a1a1a;
  border-radius: 8px;
  border: 1px solid transparent;
  cursor: pointer;
  font-family: inherit;
  font-size: 1em;
  font-weight: 500;
  margin-bottom: 10px;
  padding: 0.6em 1.2em;
  transition: border-color 0.25s;
  width: 250px;
}

li:hover {
  background-color: #ccc;
  color: #333;
}

.options-container {
  display: flex;
  justify-content: center;
}
</style>
