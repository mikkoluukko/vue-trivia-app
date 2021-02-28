<template>
  <div id="app">
    <Header 
      v-if="questions.length && !isGameOver"
      :questionsCorrect="questionsCorrect"
      :currentQuestion="index"
      :questionsTotal="questions.length"
    />
    <b-container class="bv-example-row">
      <b-row align-h="center">
        <b-col sm="9">
          <StartScreen 
            v-if="questions.length === 0" 
            :loadQuestions="loadQuestions"
          />
          <QuestionBox
            v-if="questions.length && !isGameOver && isNormalMode"
            :currentQuestion="questions[index]"
            :nextQuestion="nextQuestion"
            :increment="increment"
            :addSelectedAnswer="addSelectedAnswer"
          />
          <QuestionBoxSpeedMode
            v-if="questions.length && !isGameOver && !isNormalMode"
            :currentQuestion="questions[index]"
            :nextQuestion="nextQuestion"
            :increment="increment"
            :addSelectedAnswer="addSelectedAnswer"
          />
          <ScoreScreen 
            v-if="isGameOver"
            :score="questionsCorrect * 10"
            :questions="questions"
            :selectedAnswers="selectedAnswers"
          />
          <Footer 
            v-if="questions.length" 
            :resetGame="resetGame"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import StartScreen from './components/StartScreen';
import Header from './components/Header';
import Footer from './components/Footer';
import QuestionBox from './components/QuestionBox';
import QuestionBoxSpeedMode from './components/QuestionBoxSpeedMode';
import ScoreScreen from './components/ScoreScreen';

export default {
  name: 'App',
  components: {
    StartScreen,
    Header,
    Footer,
    QuestionBox,
    QuestionBoxSpeedMode,
    ScoreScreen,
  },
  data() {
    return {
      questions: [],
      selectedAnswers: [],
      index: 0,
      questionsCorrect: 0,
      questionsAnswered: 0,
      isNormalMode: true,
      isGameOver: false,
    }
  },
  methods: {
    loadQuestions(amount, category, difficulty, mode) {
      this.initGame(mode);
      fetch(`https://opentdb.com/api.php?amount=${amount}${category}${difficulty}`, {
        method: 'get',
      }).then((response) => {
        return response.json();
      })
      .then((jsonData) => {
        this.questions = jsonData.results;
      });
    },
    initGame(mode) {
      if (mode === "mode=normal") {
        this.isNormalMode = true;
      } else {
        this.isNormalMode = false;
      }
    },
    resetGame() {
      this.questions = [];
      this.index = 0;
      this.questionsCorrect = 0;
      this.questionsAnswered = 0;
      this.isGameOver = false;
    },
    nextQuestion() {
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
    },
    addSelectedAnswer(selectedAnswer) {
      this.selectedAnswers.push(selectedAnswer);
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
}
</style>
