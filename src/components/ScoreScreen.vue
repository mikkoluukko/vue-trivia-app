<template>
  <div class="score-container">
    <h1 class="my-4">GAME OVER</h1>
    <h2 class="my-4">Your score is: {{ score }} points</h2>
    <h3>Your stats:</h3>
    <b-table striped hover :items="items"></b-table>
  </div>
</template>

<script>
export default {
  props: {
    score: Number,
    questions: Object,
    selectedAnswers: Object,
  }, 
  data() {
    return {
      items: []      
    }
  },
  mounted() {
    for (const [index, question] of this.questions.entries()) {
      this.items.push({
        question: question.question, 
        correctAnswer: question.correct_answer, 
        yourAnswer: this.selectedAnswers[index]
      });
    }
  }
}
</script>

<style>
h1 {
  font-size: 70px;
}
</style>