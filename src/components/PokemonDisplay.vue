<template>
  <div class="px-6 md:px-10 lg:px-16 xl:px-20">
    <div v-if="pokemon && pokemon.id" class="mb-2">
      <span class="text-white font-bold text-xl"> #{{ pokemon.id }}</span>
    </div>
    <div v-if="pokemon">
      <span class="text-white font-bold text-4xl capitalize">{{ pokemon.name }}</span>
    </div>
  </div>

  <div v-if="pokemon" class="flex flex-col md:flex-row justify-center items-center md:gap-16 lg:gap-20 xl:gap-24">
    <div>
      <img class="h-64 md:h-96 xl:h-128" :src="pokemon.sprites?.other['official-artwork'].front_default" alt=""
           srcset="" ref="pokemonImage">
    </div>

    <div>
      <h1>
        teste
      </h1>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    pokemon: {
      type: Object,
      required: true,
    },
  },
};
</script>
