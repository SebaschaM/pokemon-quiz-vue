<template>
    <div class="options-container">
        <button :disabled="isDisabled" v-for="pokemon in pokemons" :key="pokemon.id"
            @click="$emit('selection', pokemon.id)">
            {{ pokemon.name }}</button>
    </div>
</template>

<script>
export default {
    props: {
        pokemons: {
            type: Array,
            required: true
        },
        isDisabled: {
            type: Boolean,
            default: false
        }
    }
}
</script>

<style scoped>
button {
    background-color: white;
    border-radius: 5px;
    border: 1px solid rgba(0, 0, 0, 0.2);
    cursor: pointer;
    margin-bottom: 10px;
    width: 250px;
    padding: 1rem;
}

button:hover {
    background-color: rgba(0, 0, 0, 0.05);
}

.options-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
}
</style>