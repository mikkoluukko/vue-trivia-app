<template>
  <div id="app">
    <Header 
      :resetGame="resetGame"
      :questionsCorrect="questionsCorrect"
      :currentQuestion="index"
      :questionsTotal="questions.length"
    />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <StartScreen 
            v-if="questions.length === 0" 
            :loadQuestions="loadQuestions"
          />
          <QuestionBox
            v-if="questions.length && !isGameOver"
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
          />
          <ScoreScreen 
            v-if="isGameOver"
            :score="questionsCorrect * 10"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import StartScreen from './components/StartScreen';
import Header from './components/Header';
import QuestionBox from './components/QuestionBox';
import ScoreScreen from './components/ScoreScreen';

export default {
  name: 'App',
  components: {
    StartScreen,
    Header,
    QuestionBox,
    ScoreScreen,
  },
  data() {
    return {
      questions: [],
      index: 0,
      questionsCorrect: 0,
      questionsAnswered: 0,
      isGameOver: false,
    }
  },
  methods: {
    loadQuestions(amount, category, difficulty) {
      fetch(`https://opentdb.com/api.php?amount=${amount}${category}${difficulty}`, {
        method: 'get',
      }).then((response) => {
        return response.json();
      })
      .then((jsonData) => {
        this.questions = jsonData.results
      });
    },
    resetGame() {
      this.questions = [];
      this.index = 0;
      this.questionsCorrect = 0;
      this.questionsAnswered = 0;
      this.isGameOver = false;
    },
    next() {
      if (this.index < this.questions.length - 1) {
        this.index++;
      } else {
        this.isGameOver = true;
      }
      
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.questionsCorrect++;
      }
      this.questionsAnswered++;
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
