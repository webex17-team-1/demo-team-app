<template>
  <h1>Vue メモ</h1>
  <div class="memo-list">
    <ul
      class="memo-list__container"
      v-for="(memo, index) in memos"
      :key="index"
    >
      <li class="memo">
        <div class="memo__checkbox">
          <input type="checkbox" v-model="memo.isDone" />
        </div>
        <div v-if="memo.isDone" class="memo__text memo__text--done">
          {{ memo.text }}
        </div>
        <div v-else class="memo__text">{{ memo.text }}</div>
        <button class="memo__delete" @click="deleteMemo(index)">削除</button>
      </li>
    </ul>
    <div class="add-memo-field">
      <input class="add-memo-field__input" type="text" v-model="inputMemo" />
      <button class="add-memo-field__button" @click="addMemo">追加</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputMemo: "",
      memos: [],
    }
  },
  methods: {
    addMemo() {
      const memo = {
        text: this.inputMemo,
        isDone: false,
      }
      this.memos.push(memo)
      this.inputMemo = ""
      localStorage.memos = JSON.stringify(this.memos)
    },
    deleteMemo(index) {
      this.memos.splice(index, 1)
      localStorage.memos = JSON.stringify(this.memos)
    },
  },
  mounted() {
    if (localStorage.memos) {
      this.memos = JSON.parse(localStorage.memos)
    }
  },
  watch: {
    memos: {
      handler() {
        localStorage.memos = JSON.stringify(this.memos)
      },
      deep: true,
    },
  },
}
</script>

<style scoped>
.memo-list {
  padding-left: 5rem;
  padding-right: 5rem;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  /* width: 200px; */
  max-width: 512px;
  margin-left: auto;
  margin-right: auto;
}

.memo-list__container {
  padding: 0;
}

.memo {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem;
  border-radius: 5px;
}

.memo:hover {
  color: white;
  background-color: #b23b61;
}

.memo__text {
  margin-left: 2rem;
  text-align: left;
}

.memo__text--done {
  text-decoration-line: line-through;
}

.memo__delete {
  margin-left: 1rem;
  padding: 0.5rem 0.5rem;
  border: solid 1px black;
  border-radius: 5px;
  background-color: white;
}

.memo__delete:hover {
  background-color: #b2ae3b;
  border-radius: 5px;
}

.add-memo-field {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.add-memo-field__input {
  padding: 10px;
}
.add-memo-field__button {
  padding: 0.5rem 0.5rem;
  border: solid 1px black;
  border-radius: 5px;
  background-color: white;
}

.add-memo-field__button:hover {
  background-color: #b2ae3b;
  border-radius: 5px;
}
</style>
