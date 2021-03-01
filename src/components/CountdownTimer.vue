<template>
  <div>
    <b-progress class="mt-2" :max="max" height="2rem">
      <b-progress-bar :value="value" variant="danger"></b-progress-bar>
    </b-progress>
  </div>
</template>

<script>
export default {
  props: {
    selectAnswer: Function,
    currentQuestion: Object,
  },
  data() {
    return {
      timer: null,
      value: 0,
      max: 100,
    };
  },
  mounted() {
    this.startTimer();
  },
  methods: {
    // If time runs out then call parent's selectAnswer with null index
    startTimer() {
      this.value = 0;
      this.timer = setInterval(() => {
        this.value += 0.5;
        if (this.value >= 100) {
          clearInterval(this.timer);
          this.selectAnswer(null);
        }
      }, 20);
    },
    stopTimer() {
      clearInterval(this.timer);
      this.value = 0;
    },
  },
};
</script>

<style>
.progress-bar {
  transition: none;
}
</style>
