<template>
  <h1>Vue クイズ</h1>
  <div class="app">
    <h2>Q. {{ quiz.text }}</h2>
    <img
      class="quiz-image"
      src="https://via.placeholder.com/300x300"
      alt="クイズタイトル"
    />
    <div class="container">
      <button>
        {{ quiz.choises[0].text }}
      </button>
      <button>
        {{ quiz.choises[1].text }}
      </button>
      <button>
        {{ quiz.choises[2].text }}
      </button>
    </div>
    <div>{{ "答え" }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      quiz: {
        text: "このキャラクターは誰でしょう",
        image: "",
        choices: [
          {
            text: "リツコ",
          },
          {
            text: "綾波レイ",
          },
          {
            text: "アスカ",
          },
        ],
      },
    }
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
