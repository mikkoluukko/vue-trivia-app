<template>
  <div class="question-box-container">
    <b-jumbotron class="my-4" bg-variant="light" border-variant="dark">
      <template #lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-2" />
      <b-list-group>
        <b-list-group-item
          class="my-1"
          v-for="(answer, index) in answers"
          :key="index"
          @click="selectAnswer(index)"
          :class="[answerClass(index)]"
          :disabled="isAnswered === true"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>

      <b-button
        variant="success"
        @click="nextQuestion"
        :disabled="isAnswered === false"
      >
        Next
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from 'lodash';

export default {
  props: {
    currentQuestion: Object,
    nextQuestion: Function,
    increment: Function,
    addSelectedAnswer: Function,
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      isAnswered: false,
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
        this.isAnswered = false;
      },
    },
  },
  methods: {
    answerClass(index) {
      let answerClass = '';
      if (this.isAnswered && this.correctIndex === index) {
        answerClass = 'correct';
      } else if (
        this.isAnswered &&
        this.selectedIndex === index &&
        this.correct_answer !== index
      ) {
        answerClass = 'wrong';
      }
      return answerClass;
    },
    selectAnswer(index) {
      this.selectedIndex = index;
      this.isAnswered = true;
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
      this.addSelectedAnswer(this.answers[this.selectedIndex]);
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

.btn {
  margin: 5px;
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
