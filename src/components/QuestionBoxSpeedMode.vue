<template>
  <div class="question-box-container">
    <b-jumbotron class=my-4 bg-variant="light" border-variant="dark">
      <template #lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4" />
      <b-list-group>
        <b-list-group-item
          class="my-1"
          v-for="(answer, index) in answers"
          :key="index"
          @click="selectAnswer(index)"
          :class="[answerClass(index)]"
          :disabled="answered === true"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>
      
      <CountdownTimer
        ref="countdownTimer"
        :handleTimerFull="handleTimerFull"
        :currentQuestion="currentQuestion"
      />
    </b-jumbotron>
  </div>
</template>

<script>
import _ from 'lodash';
import CountdownTimer from './CountdownTimer';

export default {
  components: {
    CountdownTimer,
  },
  props: {
    currentQuestion: Object,
    nextQuestion: Function,
    increment: Function,
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      answered: false,
    };
  },
  computed: {
    answers() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ];
      answers = _.shuffle(answers);
      return answers;
    },
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.answered = false;
        // This is to prevent the unneccessary call on the first question
        // when $refs.countdownTimer is still undefined
        if (this.$refs.countdownTimer != undefined) {
          this.$refs.countdownTimer.startTimer();
        }
      },
    },
  },
  methods: {
    answerClass(index) {
      let answerClass = '';
      if (this.answered && this.correctIndex === index) {
        answerClass = 'correct';
      } else if (
        this.answered &&
        this.selectedIndex === index &&
        this.correct_answer !== index
      ) {
        answerClass = 'wrong';
      }
      return answerClass;
    },
    selectAnswer(index) {
      this.$refs.countdownTimer.stopTimer();
      this.selectedIndex = index;
      this.answered = true;
      this.checkAnswer();
    },
    checkAnswer() {
      this.correctIndex = this.answers.indexOf(
        this.currentQuestion.correct_answer
      );
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.increment(isCorrect);
      setTimeout(() => {
        this.nextQuestion()
      }, 700);
    },
    handleTimerFull() {
      this.selectAnswer(null);      
    },
  },
};
</script>

<style scoped>
.list-group {
  margin-bottom: 15px;
}

.list-group-item {
  border: 1px solid gray;
}

.list-group-item:hover {
  background: #eee;
  cursor: pointer;
}

.correct {
  background-color: green;
  color: white;
}

.wrong {
  background-color: red;
  color: white;
}
</style>
