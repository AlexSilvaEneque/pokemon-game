<template>
    <ul>
        <li v-for="pokemon in options"
            :key="pokemon.id"
            @click="$emit('selection', pokemon.id), clic(pokemon.id)"
            :class="{ select: (select === pokemon.id), disabled: count > 0, list : !(select === pokemon.id) }"
            >
            {{pokemon.name}}
        </li>
    </ul>
</template>

<script>
export default {
    props: {
        options: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            select: null,
            count: 0
        }
    },
    methods: {
        clic(id) {
            this.count++
            this.select = id
        }
    }
}
</script>

<style scoped>

    ul {
        list-style: none;
    }

    .list {
        background-color: white;
        border: solid 1px;
        border-radius: 12px;
        cursor: pointer;
        margin-bottom: .8rem;
        margin-left: auto;
        margin-right: auto;
        padding: .6rem;
        width: 300px;
    }

    .list:hover {
        background-color: rgba(0, 0, 0, 0.1);
    }

    .disabled {
        pointer-events: none;
        opacity: .6;
    }

    .select {
        background-color: red;
        border: solid 1px;
        border-radius: 12px;
        cursor: pointer;
        margin-bottom: .8rem;
        margin-left: auto;
        margin-right: auto;
        padding: .6rem;
        width: 300px;
    }
</style>