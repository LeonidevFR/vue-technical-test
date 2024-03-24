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
</style>
