<template>
  <div>
    <b-row class="justify-content-md-center mt-4">
      <b-col col lg="2">Score: {{ questionsCorrect * 10 }}</b-col>
      <b-col col lg="2">Question: {{ currentQuestion + 1 }} / {{ questionsTotal }}</b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  props: {
    questionsCorrect: Number,
    currentQuestion: Number,
    questionsTotal: Number,
  }
}
</script>

<style>
.col {
  font-size: 30px;
}
</style>