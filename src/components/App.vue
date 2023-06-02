<template>
  <div :style="{ backgroundColor: pokemonBgColor }" class="flex flex-col items-center justify-center h-screen w-full">
    <div class="py-16 md:py-20 lg:py-24 xl:py-20 w-full">
      <pokemon-display :pokemon="pokemon"></pokemon-display>
    </div>

    <div class="mt-8 md:mt-10 lg:mt-12 xl:mt-14">
      <pokemon-search @pokemon-loaded="pokemonLoaded"></pokemon-search>
    </div>
  </div>
</template>

<script>
import PokemonSearch from './PokemonSearch.vue';
import PokemonDisplay from './PokemonDisplay.vue';
import ColorThief from "colorthief";

export default {
  components: {
    PokemonSearch,
    PokemonDisplay,
  },
  data() {
    return {
      pokemon: null,
      pokemonBgColor: '',
    };
  },
  methods: {
    pokemonLoaded(pokemon) {
      this.pokemon = pokemon;
      this.updatePokemonBgColor();
    },
    updatePokemonBgColor() {
      if (this.pokemon) {
        const imageUrl = this.pokemon.sprites?.other['official-artwork'].front_default;
        const img = new Image();
        img.src = imageUrl;
        img.crossOrigin = 'Anonymous';
        img.addEventListener('load', () => {
          const colorThief = new ColorThief();
          const color = colorThief.getColor(img);
          this.pokemonBgColor = `rgb(${color[0]}, ${color[1]}, ${color[2]})`;
        });
      } else {
        this.pokemonBgColor = '';
      }
    },
  },
};
</script>
