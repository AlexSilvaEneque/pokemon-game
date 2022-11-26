<template>

  <Attempts :attempt="attempts" v-if="attempts < 6" />

  <Resumen :correct="correct" :failed="failed" v-else/>
  <!-- <template v-if="!auxDelay">
    <div  class="wrapper_loading">
      <load />
    </div>
  </template> -->
  <div v-if="attempts < 6">
    <h1 v-if="!pokemon">Espere</h1>
    <div v-else>
      <h1>¿Quién es este pokemón?</h1>
      
      <pokemon-picture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
    
      <pokemon-options :options="pokemonsArr"
        @selection="checkAnswer" />
        
      <template v-if="showAnswer">
        <h2 class="fade-in">{{ msg }}</h2>
        <button @click="nextOptions" class="btn_next">Siguiente</button>
      </template>
    </div>
  </div>
  <template v-else>
    <button @click="newGame" class="btn_new">Jugar otra vez</button>
  </template>
</template>

<script>
import PokemonPicture from '@/components/PokemonPicture'
import PokemonOptions from '@/components/PokemonOptions'
import Load from '@/components/Load'
import Attempts from '@/components/Attempts.vue'
import Resumen from '@/components/Resumen.vue'

import getPokemonOptions from '@/helpers/getPokemonOptions'

export default {
    components: {
        PokemonPicture,
        PokemonOptions,
        Load,
        Attempts,
        Resumen
    },

    data() {
      return {
        pokemonsArr: [],
        pokemon: null,
        showPokemon: false,
        showAnswer: false,
        msg: null,
        auxDelay: false,
        attempts: 1,
        correct: 0,
        failed: 0
      }
    },

    methods: {

      async mixPokemonArray() {
        this.pokemonsArr = await getPokemonOptions()

        const rndInt = Math.floor(Math.random() * 4) // 0 - 3
        this.pokemon = this.pokemonsArr[rndInt]
      },

      checkAnswer(selectedId) {
        this.showPokemon = true
        this.showAnswer = true

        if (selectedId === this.pokemon.id) {
          this.correct++
          this.msg = `Correcto, ${this.pokemon.name}`
        }
        else {
          this.failed++
          this.msg = `Ups, era ${this.pokemon.name}`
        }
      },

      async nextOptions() {
        this.pokemonsArr = []
        this.showPokemon = false
        this.showAnswer = false
        this.msg = null
        this.pokemon = null

        this.attempts++

        await this.mixPokemonArray()
      },

      async newGame() {
        this.pokemonsArr = []
        this.showPokemon = false
        this.showAnswer = false
        this.msg = null
        this.pokemon = null

        this.attempts = 1
        this.correct = 0
        this.failed = 0

        await this.mixPokemonArray()
      }
    },

    mounted() {
      this.mixPokemonArray()
    }
}
</script>

<style scoped>

  .wrapper_loading {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100%;
  }
</style>