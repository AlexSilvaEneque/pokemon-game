<template>
    <img src="/pokemon_96.png" alt="" class="load">
</template>

<style scoped>
    .load {
        animation: up infinite .6s ease-in-out alternate;
    }

    @keyframes up {
        0% { transform: translateX(-20px); }
        100% { transform: translateX(40px); }
    }
</style>