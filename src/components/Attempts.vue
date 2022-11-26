<template>
    <div class="header">
        <div class="right">
            <h1>Nro Intentos: {{ attempt }}/5</h1>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        attempt: {
            type: Number,
            required: true
        }
    }
}
</script>

<style scoped>
    .popup {
        border: solid;
        margin-left: auto;
        margin-right: auto;
        width: 80%;
        height: 500px;
        
    }
</style>