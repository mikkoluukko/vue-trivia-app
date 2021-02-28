<template>
  <div class="score-container">
    <h1 class="my-4">GAME OVER</h1>
    <h2 class="my-4">Your score is {{ score }}</h2>
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
.score-container {
  margin-top: 25%;
}
h1 {
  font-size: 70px;
}
</style>