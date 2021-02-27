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
    handleTimerFull: Function,
    currentQuestion: Object,
  },
  data() {
    return {
      timer: null,
      value: 0,
      max: 100,      
    }
  },
  mounted() {
    this.startTimer();  
  },
  methods: {
    startTimer() {
      this.value = 0;      
      this.timer = setInterval(() => {
        this.value += 0.5;
        if (this.value >= 100) {
          clearInterval(this.timer);
          this.handleTimerFull();     
        } 
      }, 25);
    },
    stopTimer() {
      clearInterval(this.timer);
    }
  }
}
</script>

<style>
.progress-bar {
  transition: none;
  /* height: 2rem; */
}
</style>