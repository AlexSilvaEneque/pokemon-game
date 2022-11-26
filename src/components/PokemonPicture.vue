<template>
    <div class="pokemon-container">
        <img v-if="!showPokemon"
            :src="imgSrc"
            class="hidden-pokemon"
          alt="pokemon">

        <img v-else
            :src="imgSrc"
            class="fade-in"
            alt="pokemon">
    </div>
</template>

<script>
export default {
    props: {
        pokemonId: {
            type: Number,
            required: true
        },
        showPokemon: {
            type: Boolean,
            required: true,
            default: false
        }
    },
    computed: {
        imgSrc() {
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`
        }
    }
}
</script>

<style scoped>

    .pokemon-container {
        height: 200px;
        display: flex;
        justify-content: center;
    }

    img {
        height: 200px;
        user-select: none;
        -webkit-user-select: none;
        -webkit-user-drag: none;
    }

    .hidden-pokemon {
        filter: brightness(0);
    }
</style>