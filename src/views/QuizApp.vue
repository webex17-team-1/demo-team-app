<template>
  <h1>Vue クイズ</h1>
  <div class="app">
    <h2>Q. {{ quizs[quiz_num].text }}</h2>
    <img class="quiz-image" v-bind:src="quizImagePath" alt="クイズタイトル" />
    <div class="container">
      <button
        v-for="(choice, i) in quizs[quiz_num].choices"
        v-bind:key="i"
        v-on:click="choiced(choice)"
      >
        {{ choice.text }}
      </button>
    </div>
    <div>{{ feedback }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      feedback: "",
      quiz_num: 0,
      quizs: [
        {
          text: "このキャラクターは誰でしょう",
          image: "rei.jpg",
          choices: [
            {
              text: "リツコ",
              isCorrect: false,
              feedback: "残念。リツコはもっと年をっています。",
            },
            {
              text: "綾波レイ",
              isCorrect: true,
              feedback: "正解。この写真は綾波レイです。",
            },
            {
              text: "アスカ",
              isCorrect: false,
              feedback: "残念。アスカは",
            },
          ],
        },
        {
          text: "1枚目の写真の信頼度は何%でしょうか",
          image: "rei.jpg",
          choices: [
            {
              text: "15%",
              isCorrect: false,
              feedback: "残念。もっとアツいです。",
            },
            {
              text: "67%",
              isCorrect: false,
              feedback: "残念。もう少しアツいです。",
            },
            {
              text: "83%",
              isCorrect: true,
              feedback: "正解。こんなに信頼度高いけど、意外と外れます",
            },
          ],
        },
      ],
    }
  },
  methods: {
    choiced(choice) {
      this.feedback = choice.feedback
      if (choice.isCorrect && this.quiz_num != length(this.quizs) - 1) {
        this.quiz_num += 1
      }
    },
  },
  computed: {
    quizImagePath() {
      return "./assets/" + this.quiz.image
    },
  },
}
</script>

<style>
.app {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.quiz-image {
  height: 300px;
  width: 300px;
  object-fit: contain;
}

.container {
  display: flex;
  height: 2em;
  width: 300px;
  padding: 1em;
  justify-content: space-around;
}
</style>
