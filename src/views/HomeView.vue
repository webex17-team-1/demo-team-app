<template>
  <h1>Home</h1>
  <div class="all">
    <nav>
      <router-link
        to="/quiz"
        class="navigation__link"
        exact-active-class="navigation__link--exact-active"
        >Vue クイズ</router-link
      >|
      <router-link
        to="/palette"
        class="navigation__link"
        exact-active-class="navigation__link--exact-active"
        >Vue パレット</router-link
      >|
      <router-link
        to="/memo"
        class="navigation__link"
        exact-active-class="navigation__link--exact-active"
        >Vue メモ</router-link
      >
    </nav>
  </div>
</template>

<style scoped>
.all {
  text-align: center;
}
</style>
