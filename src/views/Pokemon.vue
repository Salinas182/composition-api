<template>
  <h1 v-if="!pokemon && !errorMessage">Buscando...</h1>
  <h1 v-else-if="errorMessage">{{ errorMessage }}</h1>
  <template v-else>
    <h3>{{ pokemon.name }}</h3>
    <img :src="pokemon.sprites.front_default" :alt="pokemon.name">
    <br>
    <router-link :to="{ name: 'pokemon-search' }">Return</router-link>
  </template>
</template>

<script>

import { watch } from 'vue'
import { useRoute, onBeforeRouteLeave } from 'vue-router'
import usePokemon from '@/composables/usePokemon'

export default {
  setup() {
    const route = useRoute()
    const { pokemon, isLoading, errorMessage, searchPokemon } = usePokemon(route.params.id)

    watch(
      () => route.params.id,
      () => {
        searchPokemon(route.params.id)
      }
    )

    onBeforeRouteLeave(() => {
      const userChoice = window.confirm('Are you sure you want to leave?')
      return userChoice
    })

    return {
      pokemon,
      isLoading,
      errorMessage,
      searchPokemon
    }
  }
}
</script>
