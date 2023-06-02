<template>
    <div class="flex flex-col md:flex-row gap-4">
        <div class="flex flex-col md:flex-row gap-4">
            <input type="text" v-model="pokemonName" @keyup.enter="pokemonSearch"
                class="flex items-center justify-center bg-gray-300 h-10 p-4 outline-none rounded-lg">
            <button class="flex items-center justify-center w-16 h-10 bg-gray-300 rounded-xl"
                @click="pokemonSearch">Go!</button>
        </div>
    </div>
</template>
  
  
  
<script>
export default {
    data() {
        return {
            pokemonName: null,
        }
    },
    methods: {
        pokemonSearch() {
            fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokemonName}`)
                .then(response => {
                    if (!response.ok) {
                        throw new Error(alert(`Pokemon não existe: ${this.pokemonName}`));
                    }
                    return response.json();
                })
                .then(data => {
                    this.$emit('pokemon-loaded', data);
                    console.log(data);
                })
                .catch(error => {
                    console.error(error);
                })
        }
    }
}
</script>
  