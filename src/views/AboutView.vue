<template>
  <div class="about">
    <div
        v-if="pokemon"
        class="w-6/12 m-auto bg-purple-100 mt-4 shadow-2xl flex justify-center flex-col items-center"
    >
      <h3 class="text-2xl text-green-900 uppercase">{{ pokemon.name }}</h3>
      <div class="flex justify-center">
        <img class="w-48" :src="pokemon.sprites.front_shiny" alt="" />
        <img class="w-48" :src="pokemon.sprites.back_shiny" alt="" />
      </div>
      <h3  class="text-yellow-400">Types</h3>
      <div v-for="(type, idx) in pokemon.types" :key="idx">
        <h5 class="text-blue-900">{{type.type.name}}</h5>
      </div>
    </div>
    <div v-else class="text-black bg-red-500 justify-center h-24 m-auto p-4">
      لايوجد اسم بهذه الشيء او الصورة غير موجوده
    </div>
  </div>
</template>

<script>
import { reactive, toRefs } from "vue";
import { useRoute } from "vue-router";
export default {
  setup() {
    const route = useRoute();
    const pokemon = reactive({
      pokemon: null
    });
    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
        .then((res) => res.json())
        .then((data) => {
          pokemon.pokemon = data;
          console.log(data);
        });
    return { ...toRefs(pokemon) };
  }
};
</script>