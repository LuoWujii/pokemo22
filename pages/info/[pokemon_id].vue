<script  lang="ts" setup>
// import { useRoute } from 'vue-router'
// const route = useRoute()
// const id = route.params.id

const { pokemon_id } = useRoute().params
// const id = ref(pokemon_id as any * 1)

const { data } = await useFetch<any>(`https://pokeapi.co/api/v2/pokemon/${pokemon_id}`,{
 method: 'GET'
})

// const { data: next } = await useFetch<any>(`https://pokeapi.co/api/v2/pokemon/${id.value + 1}`,{
//  method: 'GET'
// })

// const { data: prev } = await useFetch<any>(`https://pokeapi.co/api/v2/pokemon/${id.value - 1}`,{
//  method: 'GET'
// })

console.log(data.value);

function capitalizeFirstLetter(string) {
    return string.charAt(0).toUpperCase() + string.slice(1);
}

// const nextPrev = (type: 'next' | 'prev') =>{
//     if(type == 'next') {
//       useRouter().push({ name: 'info-pokemon_id', params: {pokemon_id: (id.value + 1)  } })
//     } else {
//         useRouter().push({ name: 'info-pokemon_id', params: {pokemon_id: (id.value - 1)  } })
        
//     }
// }

</script>

<template>
    <div class="p-4 mx-auto ">
        <PokemoProfileCard class="mx-auto py-6 px-6 ">
         <div class=" pb-24 flex-col w-full items-center flex">
            <p class="honk-as text-xl">EXP</p>
            <h1 class="honk-as text-6xl">{{ data.base_experience }}</h1>
         </div>
            <div class="bg-white w-full h-[400px]  items-center rounded-lg shadow-lg">
<div class="relative flex justify-center">
    <div class="flex absolute justify-center -top-24 gap-3"> 
        <img src="/assets/img/shadow.png " class=" -top-3 w-52 h-52 absolute" alt="">
        <img class=" z-40 w-36 h-36 rounded-full"
        :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon_id}.png`" alt="">
    </div>
</div>
                <div class="flex w-full justify-center pt-16 pb-5 items-center">
                    <h1 class="bungee-spice-regular text-3xl">{{ data.name }}</h1>
                </div>
                <div class="flex w-full justify-center gap-3">
                    
                    <div class="gap-3 mx-auto flex flex-col items-center">
                           <h1 class="honk-as text-2xl">{{ data.weight / 10 + ' kg' }}</h1> 
                          
                           <p class="text-xs text-gray-400">Weight</p>
                    </div>
                   <p class=" divide-y-2 w-auto border"></p>
                    <div class="gap-3 mx-auto items-center flex flex-col">
                           <h1 class="honk-as text-2xl">{{ data.height / 10 + ' m'}}</h1> 
                           <p class="text-xs text-gray-400">Height</p>
                    </div>
                </div>
                <p class="pl-2 text-gray-400 text-xs pt-5 ">Abilities:</p>
                <div class="flex justify-center gap-4 py-1">
                    
                       <h1 v-for="({ability}, index) in data.abilities" :key="index" 
                       class="bungee-spice-regular  rounded-full px-2 py-1 "> {{ ability.name }}</h1>
                    </div>
                    
                    <p class="divide-x-8 border w-auto"></p>
                <p class="pl-2 text-gray-400 text-xs pt-5 ">Types:</p>
                <div class="flex justify-center gap-4 py-1">
                    
                       <h1 v-for="({type}, index) in data.types" :key="index" 
                       class="bungee-spice-regular  rounded-full px-2 py-1 "> {{ type.name }}</h1>
                       
                    </div>
                    
                    <p class="divide-x-8 border w-auto"></p>
                </div>
                

     

            
                <!-- <div  v-for="sprite, key,index in data.sprites" :key="index">
                    <img :src="data.sprites[key]" alt="">
                </div> -->
                <!-- <NuxtLink :to="{ name: 'info-pokemon_id', params: {pokemon_id: id - 1 } }" 
             class="flex justify-center rounded-lg shadow-sm hover:shadow-md transition ease-linear hover:scale-105
             flex-col items-center px-4 w-auto my-2 py-2 bg-black bg-opacity-5">
                <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${id - 1}.png`" alt="">
                <h1 class="text-lg font-semibold">{{ capitalizeFirstLetter(prev.name) }}</h1>
            </NuxtLink>
                <NuxtLink :to="{ name: 'info-pokemon_id', params: {pokemon_id: id + 1 } }" 
             class="flex justify-center rounded-lg shadow-sm hover:shadow-md transition ease-linear hover:scale-105
             flex-col items-center px-4 w-auto my-2 py-2 bg-black bg-opacity-5">
                <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${id + 1}.png`" alt="">
                <h1 class="text-lg font-semibold">{{ capitalizeFir stLetter(next.name) }}</h1>
            </NuxtLink> -->
            
        </PokemoProfileCard>
    </div>
</template>


<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Honk&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Bungee+Spice&family=Honk&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Bungee+Spice&family=Honk&family=Nabla&display=swap');
.honk-as {
  font-family: "Honk", system-ui;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;
  font-variation-settings:
    "MORF" 15,
    "SHLN" 50;

}
.bungee-spice-regular {
  font-family: "Bungee Spice", sans-serif;
  font-weight: 400;
  font-style: normal;
}
.nabla-d {
  font-family: "Nabla", system-ui;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;
  font-variation-settings:
    "EDPT" 100,
    "EHLT" 12;
}
</style>