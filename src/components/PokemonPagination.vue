<template>
    <div class="flex justify-center items-center my-8">
        <button @click="previousPage" :disabled="currentPage === 1">Previous</button>
        <span class="mx-4">{{ currentPage }}</span>
        <button @click="nextPage" :disabled="currentPage === totalPages">Next</button>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            currentPage: 1,
            totalPages: null,
            pokemons: [],
        }
    },
    methods: {
        fetchPokemons() {
            fetch(`https://pokeapi.co/api/v2/pokemon?offset=${(this.currentPage - 1) * 20}&limit=20`)
                .then(response => {
                    if (!response.ok) {
                        throw new Error('Erro ao buscar pokemons');
                    }
                    return response.json();
                })
                .then(data => {
                    this.totalPages = Math.ceil(data.count / 20);
                    this.pokemons = data.results;
                })
                .catch(error => {
                    console.error(error);
                });
        },
        previousPage() {
            if (this.currentPage > 1) {
                this.currentPage--;
                this.fetchPokemons();
            }
        },
        nextPage() {
            if (this.currentPage < this.totalPages) {
                this.currentPage++;
                this.fetchPokemons();
            }
        },
    },
    watch: {
        pokemons: {
            handler(newPokemons) {
                this.$emit('pokemons-loaded', newPokemons);
            },
            immediate: true,
        },
    },
}
</script>
  