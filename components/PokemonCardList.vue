<script setup lang="ts">
  const { pokemon } = defineProps(['pokemon']) 

</script>
<template>
    <NuxtLink :to="{ name: 'info-pokemon_id', params: {pokemon_id: pokemon.url.split('/')[6]} }"  
            class="list-card  flex justify-center hover:shadow-md transition-all duration-300 hover:scale-105
             flex-col items-center">
             <slot />
             </NuxtLink>
</template>


<style scoped>

</style>