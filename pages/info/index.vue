<script  lang="ts" setup>

// import { useRoute } from 'vue-router'
// const route = useRoute()
// const id = route.params.id
import { useInfiniteScroll } from "@vueuse/core";


const { id } = useRoute().params

const { data, pending } = await useFetch<any>(`https://pokeapi.co/api/v2/pokemon/`,{
 method: 'GET'
})
const el = ref<HTMLElement | null>(null)
useInfiniteScroll(
    window,
    async () => {
        pending.value = true;
        const { data: moreData, pending: morePending } = await useFetch(data.value.next,{
            method: 'GET'
      });
      pending.value = morePending.value;
      data.value.results.push(...moreData.value.results)
      data.value.next = moreData.value.next;
      data.value.previous = moreData.value.previous;

    },    
    { distance: 0 } 
    )  
    
    
    function capitalizeFirstLetter(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
    }
const pokemonName = ref('');
const searchVal = computed(()=>{
    return data.value.results.filter((pokemon)=>{
        return pokemon.name.toLowerCase().includes(pokemonName.value.toLocaleLowerCase()) 
    }) 
})
</script>

<template>
    <div class="flex">
       
        <div class=" mx-auto w-auto max-w-xl p-4">
            
            <input v-model="pokemonName"
            placeholder="Search pokemon..." 
            class="rounded-full mb-4 bg-white outline-0 pl-2 px-1 text-lg py-2 shadow-md border border-gray-200 min-w-64" type="text">
            <div class="flex flex-wrap justify-center gap-y-2 gap-x-4">
                <h1 v-if="!searchVal.length">No pokemon found</h1>
                <div v-for="(pokemon, index) in searchVal" :key="index" >
                    <PokemonCardList :pokemon="pokemon">
                        <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.url.split('/')[6]}.png`" alt="">
                        <h1 class="text-lg font-semibold">{{ capitalizeFirstLetter(pokemon.name) }}</h1>
                    </PokemonCardList>
                </div>
                <div v-if="pending" class="flex flex-wrap mb-56 justify-center gap-y-2 gap-x-4" >
                    <div v-for="i in 4" :key="i" class="list-card bg-black bg-opacity-5  flex justify-center 
             flex-col items-center">
                        <div class="h-16 w-16 bg-gray-200 rounded-md"></div>
                        <div class="h-4 w-16 bg-gray-200 mt-8"></div>
                    </div>
                </div>
            </div>
            <!-- <div v-if="!pokemonName" class=" flex justify-center w-full mt-4">
                <button @click="load" class=" py-2 px-8 rounded-full text-lg border border-green-400 text-emerald-600 font-semibold hover:bg-green-100 transition-all duration-200">
                   {{ pending ? 'Loading...' : 'Load more' }} </button>
            </div> -->
        </div>
    </div>
</template>


<style scoped>

</style>