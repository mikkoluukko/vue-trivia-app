<template>
  <div>
    <h1>Start Screen</h1>
    <div>
      <select name="trivia_amount" v-model="selectedAmount">
        <option value="5">5 Questions</option>
        <option value="10">10 Questions</option>
        <option value="20">20 Questions</option>
      </select>
    </div>
    <div>
      <select name="trivia_category" v-model="selectedCategory">
        <option value="">Any Category</option>
        <option value="category=9">General Knowledge</option>
        <option value="category=10">Entertainment: Books</option>
        <option value="category=11">Entertainment: Film</option>
        <option value="category=12">Entertainment: Music</option>
        <option value="category=13">Entertainment: Musicals &amp; Theatres</option>
        <option value="category=14">Entertainment: Television</option>
        <option value="category=15">Entertainment: Video Games</option>
        <option value="category=16">Entertainment: Board Games</option>
        <option value="category=17">Science &amp; Nature</option>
        <option value="category=18">Science: Computers</option>
        <option value="category=19">Science: Mathematics</option>
        <option value="category=20">Mythology</option>
        <option value="category=21">Sports</option>
        <option value="category=22">Geography</option>
        <option value="category=23">History</option>
        <option value="category=24">Politics</option>
        <option value="category=25">Art</option>
        <option value="category=26">Celebrities</option>
        <option value="category=27">Animals</option>
        <option value="category=28">Vehicles</option>
        <option value="category=29">Entertainment: Comics</option>
        <option value="category=30">Science: Gadgets</option>
        <option value="category=31">Entertainment: Japanese Anime &amp; Manga</option>
        <option value="category=32">Entertainment: Cartoon &amp; Animations</option>		
      </select>
    </div>
    <div>
      <select name="trivia_difficulty" v-model="selectedDifficulty">
        <option value="">Any Difficulty</option>
        <option value="difficulty=easy">Easy</option>
        <option value="difficulty=medium">Medium</option>
        <option value="difficulty=hard">Hard</option>
      </select>
    </div>
    <div>
      <select name="trivia_mode" v-model="selectedMode">
        <option value="mode=normal">Normal Mode</option>
        <option value="mode=speed">Speed Mode</option>
      </select>
    </div>

    <button @click="startGame()">START GAME</button>

    
  </div>
</template>

<script>
export default {
  props: {
    loadQuestions: Function
  },
  data() {
    return {
      selectedAmount: '10',
      selectedCategory: '',
      selectedDifficulty: '',
      selectedMode: 'mode=normal'
    }
    
  },
  methods: {
    startGame() {
      let amount = this.selectedAmount;
      let category = `&${this.selectedCategory}`;
      let difficulty = `&${this.selectedDifficulty}`;
      let mode = this.selectedMode;
      this.loadQuestions(amount, category, difficulty, mode);
    }
  }
}
</script>

<style>

</style>