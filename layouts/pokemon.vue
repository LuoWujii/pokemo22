<template>
  <div>
      <header>
      <nav>
          
      </nav>
    </header>

    <div>
      <slot />
    </div>
    <footer>
      <ul>
          <li>
            <NuxtLink to="/pokemon">Pokemon</NuxtLink>
          </li>
          <li>
            <NuxtLink to="/info">Pokemon Info</NuxtLink>
          </li>
        </ul>
    </footer>
  </div>
</template>

<script setup lang="ts">

</script>

<style scoped>
.router-link-exact-active {
  color:aqua
}
</style>