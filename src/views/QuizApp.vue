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
    <div>
      <button
        id="next-button"
        v-on:click="nextQuiz"
        v-bind:disabled="isDisabled"
      >
        次の問題へ
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isDisabled: true,
      feedback: "",
      quiz_num: 0,
      quizs: [
        {
          text: "このキャラクターは誰でしょうか",
          image: require("../assets/rei.jpg"),
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
              feedback: "残念。アスカじゃないです。",
            },
          ],
        },
        {
          text: "このキャラクターは誰でしょうか",
          image: require("../assets/gendou.jpg"),
          choices: [
            {
              text: "ゲンドウ",
              isCorrect: true,
              feedback: "正解。主人公のお父さんです。",
            },
            {
              text: "冬月先生",
              isCorrect: false,
              feedback: "残念、違います。",
            },
            {
              text: "加持",
              isCorrect: false,
              feedback: "残念、違います。",
            },
          ],
        },
        {
          text: "最終問題 このキャラクターは誰でしょうか",
          image: require("../assets/kaorukun.jpg"),
          choices: [
            {
              text: "シンジ君",
              isCorrect: true,
              feedback: "残念、違います。",
            },
            {
              text: "カオル君",
              isCorrect: true,
              feedback: "正解です。",
            },
            {
              text: "加持",
              isCorrect: false,
              feedback: "残念、違います。",
            },
          ],
        },
      ],
    }
  },
  methods: {
    choiced(choice) {
      this.feedback = choice.feedback
      if (choice.isCorrect && this.quiz_num != this.quizs.length - 1) {
        this.isDisabled = false
      }
    },
    nextQuiz() {
      this.quiz_num += 1
      this.isDisabled = true
      this.feedback = ""
      if (this.quiz_num === this.quizs.length - 1) {
        const nextButton = document.getElementById("next-button")
        nextButton.remove()
      }
    },
  },
  computed: {
    quizImagePath() {
      return this.quizs[this.quiz_num].image
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
