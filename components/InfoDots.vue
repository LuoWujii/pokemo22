<script setup lang="ts">
defineProps<{
    ability: String
    
}>()
</script>

<template>
    <div class="h-14 bg-gradient-to-r from-sky-500 to-indigo-500">
      <slot />
    </div>
</template>


<style scoped>

</style>