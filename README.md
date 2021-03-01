# Vue Trivia App

## About
The goal of this project was to create a trivia game using Vue and the [Open Trivia DB API](https://opentdb.com/).

The project uses [Bootstrap Vue](https://bootstrap-vue.org/).

## Description
The game is a generic trivia quiz where each correct answer is worth 10 points.

The game consists of the following main components:
- Start Screen
- Header
- Footer
- Question Box
- Score Screen

### Start Screen
This is the screen that the user is first presented with. It has question amount, category and difficulty options that result in the corresponding questions to be fetched from the Open Trivia DB API. It also has an option to choose between a normal game mode or a speed mode.

### Header
The header is displayed during the gameplay (i.e. it is not visible in the start screen or in the score screen). It is used to display the current score and the number of the current question.

### Footer
The footer is displayed in all other screens except the start screen. It is used to display a "Back to start screen" button which resets the game and returns the user to the start screen.

### Question Box
There are two separate versions of the question box. Both versions include a box in the middle of the screen. The current question is displayed in the top part of the box and the answer options in the middle part as individual clickable boxes. In normal mode the bottom part of the box has a "Next" button that can be clicked after selecting an answer and it will load the next question. In speed mode the bottom part has a timer bar that fills up in 4 seconds unless the user selects an answer before that. In the speed mode the game automatically advances to next question after a delay of 600 ms after the user has selected an answer or after the timer bar has filled up.

### Score Screen
The score screen is displayed after all the questions have been gone through. In the score screen the user's final score is displayed along with a table of all the questions, the user's chosen answers and the correct answers to them.


## Generic Vue app instructions

### Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
