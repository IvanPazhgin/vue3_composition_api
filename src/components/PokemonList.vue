<template>
  <h3>The RESTful Pokémon API</h3>
  <div class="pokemon-list">
    <div v-for="pokemon in pokemons" :key="pokemon.name" class="pokemon-card">
      <PokemonCard :pokemon="pokemon" />
    </div>
  </div>
</template>

<script setup>
import { shallowRef, onMounted } from 'vue';
import axios from 'axios';
import PokemonCard from './PokemonCard.vue';

const pokemons = shallowRef([]);

const fetchPokemons = async () => {
  try {
    const response = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=20');
    pokemons.value = response.data.results;
  } catch (error) {
    console.error(error);
  }
};
onMounted(fetchPokemons);
</script>

<style>
.pokemon-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 16px;
}
.pokemon-card {
  flex: 0 1 calc(25% - 32px);
  box-sizing: border-box;
  border: 1px solid #ddd;
  padding: 16px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  /*width: 200px;*/
}
</style>
