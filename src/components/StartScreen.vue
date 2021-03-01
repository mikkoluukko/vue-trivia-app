<template>
  <div>
    <b-img class="my-4" :src="logo" fluid alt="Vue Trivia App Logo"></b-img>
    <b-jumbotron bg-variant="light" border-variant="dark">
      <div class="my-2">
        <b-form-select name="trivia_amount" v-model="selectedAmount">
          <b-form-select-option value="5">5 Questions</b-form-select-option>
          <b-form-select-option value="10">10 Questions</b-form-select-option>
          <b-form-select-option value="20">20 Questions</b-form-select-option>
        </b-form-select>
      </div>
      <div class="my-2">
        <b-form-select name="trivia_category" v-model="selectedCategory">
          <b-form-select-option value="">
            Any Category
          </b-form-select-option>
          <b-form-select-option value="category=9">
            General Knowledge
          </b-form-select-option>
          <b-form-select-option value="category=10">
            Entertainment: Books
          </b-form-select-option>
          <b-form-select-option value="category=11">
            Entertainment: Film
          </b-form-select-option>
          <b-form-select-option value="category=12">
            Entertainment: Music
          </b-form-select-option>
          <b-form-select-option value="category=13">
            Entertainment: Musicals &amp; Theatres
          </b-form-select-option>
          <b-form-select-option value="category=14">
            Entertainment: Television
          </b-form-select-option>
          <b-form-select-option value="category=15">
            Entertainment: Video Games
          </b-form-select-option>
          <b-form-select-option value="category=16">
            Entertainment: Board Games
          </b-form-select-option>
          <b-form-select-option value="category=17">
            Science &amp; Nature
          </b-form-select-option>
          <b-form-select-option value="category=18">
            Science: Computers
          </b-form-select-option>
          <b-form-select-option value="category=19">
            Science: Mathematics
          </b-form-select-option>
          <b-form-select-option value="category=20">
            Mythology
          </b-form-select-option>
          <b-form-select-option value="category=21">
            Sports
          </b-form-select-option>
          <b-form-select-option value="category=22">
            Geography
          </b-form-select-option>
          <b-form-select-option value="category=23">
            History
          </b-form-select-option>
          <b-form-select-option value="category=24">
            Politics
          </b-form-select-option>
          <b-form-select-option value="category=25">
            Art
          </b-form-select-option>
          <b-form-select-option value="category=26">
            Celebrities
          </b-form-select-option>
          <b-form-select-option value="category=27">
            Animals
          </b-form-select-option>
          <b-form-select-option value="category=28">
            Vehicles
          </b-form-select-option>
          <b-form-select-option value="category=29">
            Entertainment: Comics
          </b-form-select-option>
          <b-form-select-option value="category=30">
            Science: Gadgets
          </b-form-select-option>
          <b-form-select-option value="category=31">
            Entertainment: Japanese Anime &amp; Manga
          </b-form-select-option>
          <b-form-select-option value="category=32">
            Entertainment: Cartoon &amp; Animations
          </b-form-select-option>
        </b-form-select>
      </div>
      <div class="my-2">
        <b-form-select name="trivia_difficulty" v-model="selectedDifficulty">
          <b-form-select-option value="">
            Any Difficulty
          </b-form-select-option>
          <b-form-select-option value="difficulty=easy">
            Easy
          </b-form-select-option>
          <b-form-select-option value="difficulty=medium">
            Medium
          </b-form-select-option>
          <b-form-select-option value="difficulty=hard">
            Hard
          </b-form-select-option>
        </b-form-select>
      </div>
      <div class="my-2">
        <b-form-select name="trivia_mode" v-model="selectedMode">
          <b-form-select-option value="mode=normal">
            Normal Mode
          </b-form-select-option>
          <b-form-select-option value="mode=speed">
            Speed Mode
          </b-form-select-option>
        </b-form-select>
      </div>
    </b-jumbotron>
    <b-button size="lg" variant="primary" @click="startGame()">
      START GAME
    </b-button>
  </div>
</template>

<script>
export default {
  props: {
    loadQuestions: Function,
  },
  data() {
    return {
      logo: require('@/assets/logo.png'),
      selectedAmount: '10',
      selectedCategory: '',
      selectedDifficulty: '',
      selectedMode: 'mode=normal',
    };
  },
  methods: {
    startGame() {
      let amount = this.selectedAmount;
      let category = `&${this.selectedCategory}`;
      let difficulty = `&${this.selectedDifficulty}`;
      let mode = this.selectedMode;
      this.loadQuestions(amount, category, difficulty, mode);
    },
  },
};
</script>

<style></style>
