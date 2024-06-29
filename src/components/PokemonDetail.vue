<template>
  <div class="container">
    <button @click="router.push(`/`)">Назад</button>
    <div v-if="loading" style="margin: 20px 0">Загрузка данных...</div>
    <div v-if="pokemon" class="pokemon-detail">
      <h1>{{ pokemon.name }}</h1>
      <img :src="pokemon.sprites.front_default" alt="pokemon image">
      <p>Height: {{ pokemon.height }}</p>
      <p>Weight: {{ pokemon.weight }}</p>
      <p>Base experience: {{ pokemon.base_experience }}</p>
    </div>
  </div>
</template>

<script setup>
import { shallowRef, onMounted } from 'vue';
import axios from 'axios';
import {useRoute, useRouter} from 'vue-router';

const pokemon = shallowRef(null);
const loading = shallowRef(false);
const route = useRoute();
const router = useRouter();

const fetchPokemonDetail = async () => {
  try {
    loading.value = true;
    const response = await axios.get(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
    pokemon.value = response.data;
  } catch (error) {
    console.error(error);
  } finally {
    loading.value = false;
  }
};

onMounted(fetchPokemonDetail);
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin: 20px;
}

.pokemon-detail {
  text-align: left;
}
</style>
