<template>
    <h1 v-if="!pokemon">Espere por favor...</h1>
    <div v-else class="container">
        <h1>¿Quién es este Pokemon?</h1>
        <PokemonPictureVue :pokemonId="pokemon.id" :showPokemon="showPokemon" />
        <PokemonOptionsVue :pokemons="pokemonsArr" @selection="checkAnswer" :isDisabled="blockedButton" />
        <template v-if="showAnswer">
            <h2 class="fade-in"> {{ message }}</h2>
            <h3 class="fade-in">El pokemon es {{ pokemon.name }}</h3>
            <button @click="newGame" class="btn-new-game">Nuevo Juego</button>
        </template>
    </div>
    <footer>
        <p>Desarrollado por <a href="https://github.com/SebaschaM" class="profile_me" target="_blank">@Sebastian Chaquila</a></p>
    </footer>
</template>

<script>
import PokemonOptionsVue from '@/components/PokemonOptions.vue'
import PokemonPictureVue from '@/components/PokemonPicture.vue'
import getPokemonOptions from '@/helpers/getPokemonOptions';

export default {
    name: 'PokemonPageVue',
    components: {
        PokemonOptionsVue,
        PokemonPictureVue
    },
    data() {
        return {
            pokemon: null,
            pokemonsArr: [],
            showPokemon: false,
            blockedButton: false,
            showAnswer: false,
            message: ''
        }
    },
    methods: {
        async mixPokemonsArray() {
            this.pokemonsArr = await getPokemonOptions()

            const rndInt = Math.floor(Math.random() * 4)
            this.pokemon = this.pokemonsArr[rndInt]
        },
        checkAnswer(pokemonId) {
            this.showPokemon = true
            this.blockedButton = true
            this.showAnswer = true
            if (pokemonId === this.pokemon.id) {
                this.message = `¡Felicidades :) !`
            } else {
                this.message = 'Incorrecto'
            }
        },
        newGame() {
            this.showPokemon = false
            this.showAnswer = false
            this.blockedButton = false
            this.pokemon = null
            this.pokemonsArr = []
            this.mixPokemonsArray()
        }
    },
    mounted() {
        this.mixPokemonsArray()
    }
}
</script>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    row-gap: 20px;
    margin-bottom: 2rem;
}

.btn-new-game {
    background-color: #4CAF50;
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border-radius: 8px;
}

.btn-new-game:hover {
    background-color: #45a049;
}

.profile_me {
    color: #ada203;
    text-decoration: none;
}
</style>