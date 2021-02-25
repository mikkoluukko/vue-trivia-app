<template>
  <div>
    <h1>GAME OVER</h1>
    <h2>Your score is {{ score }}</h2>
  </div>
</template>

<script>
export default {
  props: {
    score: Number
  }
}
</script>

<style>

</style>