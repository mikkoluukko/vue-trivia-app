<template>
  <div class="mb-4">
    <b-button size="lg" variant="secondary" @click="resetGame">
      Back to start screen
    </b-button>
  </div>
</template>

<script>
export default {
  props: {
    resetGame: Function,
  }  
}
</script>

<style>

</style>