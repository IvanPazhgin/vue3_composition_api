<template>
  <div class="pokemon-card" @click="goToDetail">
    <h3>{{ pokemon.name }}</h3>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

// eslint-disable-next-line no-undef
const props = defineProps({
  pokemon: {
    type: Object,
    default: () => ({}),
  },
});

const router = useRouter();
const goToDetail = () => router.push(`/pokemon/${props.pokemon.name}`);
</script>

<style>
.pokemon-card {
  cursor: pointer;
  transition: transform 0.2s;
}
.pokemon-card:hover {
  transform: scale(1.05);
}
</style>
