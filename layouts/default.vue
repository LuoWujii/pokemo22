<template>
    <div>
        <header class=" w-auto bg-white shadow-md ">
        <nav class="flex" >
            <ul class=" flex justify-around  w-full text-lg font-bold my-10">
            <li class=" ">
              <NuxtLink to="/">Home</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/">Pokemon</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/info">Pokemon Info</NuxtLink>
            </li>
          </ul>
        </nav>
      </header>

      <div>
        <slot />
      </div>
    </div>
</template>

<script setup lang="ts">

</script>

<style scoped>
.router-link-exact-active {
    color:aqua
}
</style>