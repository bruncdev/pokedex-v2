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
                srcset="">
        </div>

        <div>
            <h1>
                teste
            </h1>
        </div>
    </div>
</template>
  
<script>

import ColorThief from 'color-thief-node';

export default {
    props: {
        pokemon: {
            type: Object,
            required: true,
        },
    },
    data() {
        return {
            bgColor: '',
        };
    },
    mounted() {
        this.updateBackgroundColor();
    },
    methods: {
        updateBackgroundColor() {
            const img = new Image();
            img.crossOrigin = 'Anonymous';
            img.src = this.pokemon.sprites?.other['official-artwork'].front_default;

            img.addEventListener('load', () => {
                const colorThief = new ColorThief();
                const color = colorThief.getColor(img);
                const bgColor = `rgb(${color[0]}, ${color[1]}, ${color[2]})`;
                this.bgColor = bgColor;
            });
        },
    },
};

</script>
  