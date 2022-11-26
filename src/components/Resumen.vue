<template>
  <div class="wrapper_resumen">
    <h1>Resumen</h1>
    Aciertos: {{correct}} Fallas: {{ failed }}
  </div>
</template>

<script>
export default {
    props: {
        correct: {
            type: Number
        },
        failed: {
            type: Number
        }
    }
}
</script>

<style>

</style>