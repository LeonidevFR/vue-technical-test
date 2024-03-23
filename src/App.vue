<template>
  <div id="app">
    <ArticlePage />
  </div>
</template>

<script>
import ArticlePage from "./pages/ArticlePage.vue";
import "@fortawesome/fontawesome-free/css/all.css";

export default {
  name: "App",
  components: {
    ArticlePage,
  },
};
</script>

<style lang="scss">
@import "assets/styles/app.scss";

#app {
  @extend .text--medium;
  font-family: "tt_chocolates_medium", Arial, Helvetica, sans-serif;
  height: 100%;
}
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}
body {
  margin: 0;
}
html,
body {
  width: 100%;
  height: 100%;
  background-color: #f5faff;
}
</style>
