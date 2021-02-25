<template>
  <div>
    <b-nav tabs>
      <b-nav-item active @click="resetGame">Vue Trivia Game</b-nav-item>
      <b-nav-item>Score: {{ questionsCorrect * 10 }}</b-nav-item>
      <b-nav-item v-if="questionsTotal > 0">
        Question: {{ currentQuestion + 1 }} / {{ questionsTotal }}
      </b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  props: {
    resetGame: Function,
    questionsCorrect: Number,
    currentQuestion: Number,
    questionsTotal: Number,
  }
}
</script>

<style>

</style>