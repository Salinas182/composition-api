<template>
  <h1>Buscar pokémon: {{ pokemonId }}</h1>

  <form @submit.prevent="onSubmit">
    <input 
      type="number"
      placeholder="Número de pokémon"
      v-model="pokemonId"
      ref="txtSearchId"
    >
  </form>
  <br>
  <span>Presione "Enter" para buscar</span>
  
</template>

<script>
  import { ref, onMounted } from 'vue'
  import { useRouter } from 'vue-router'
  
  export default {
    setup() {
      const router = useRouter()
      const pokemonId = ref(1)
      const txtSearchId = ref()

      onMounted(() => {
        txtSearchId.value.select()
      })

      return {
        pokemonId,
        txtSearchId,
        onSubmit: () => {
          router.push({ name: 'pokemon-id', params: { id: pokemonId.value } })
        }
      }
    }
  }
</script>
