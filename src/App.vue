
<template>
  <div class="h-screen w-full flex items-center justify-center flex-row gap-8">

    <div>
      <div>{{ data.id }} <span>{{ data.name }}</span></div>
      <img class="h-96 w-96" :src="data.sprites?.other['official-artwork'].front_default" alt="" srcset="">
    </div>

    <div class="flex flex-col gap-4">
      <input type="search" name="form.pokemonName" v-model="form.pokemonName" id="form.pokemonName"
        class="border-2 border-zinc-500 p-2 rounded-lg">
      <button v-on:click="pokemonSearch(form.pokemonName)" class="">CATCH!</button>
    </div>
  </div>
</template>


<script>
export default {

  data() {
    return {
      form: {
        pokemonName: null,
      },
      data: [],

    }
  },
  methods: {
    pokemonSearch(pokemonName) {
      fetch(`https://pokeapi.co/api/v2/pokemon/${pokemonName}`)
        .then(response => {
          if (!response.ok) {
            throw new Error('Erro ao buscar pokemons');
          }
          return response.json();
        })
        .then(data => {
          this.data = data;
          console.log(data);
        })
        .catch(error => {
          console.error(error);
        })
    }
  }
}
</script>