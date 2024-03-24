<template>
  <div>
    <div class="container" style="overflow: hidden">
      <h1 class="text--demibold font--lg main-dark" style="padding: 16px">
        Mes articles
      </h1>
      <ul style="padding: 0">
        <li
          v-for="(article, i) in articleList"
          :key="i"
          class="text--medium font--md main-light article-list__item"
          @click="$emit('onEditArticle', i)"
        >
          {{ article.name }}
          <i class="fas fa-chevron-right"></i>
        </li>
      </ul>
    </div>
    <div style="display: flex; justify-content: center; margin: 32px 0">
      <ArticleButton
        class="article-list__add-button"
        :rounded="true"
        @onClick="$emit('onAddArticle')"
      >
        +
      </ArticleButton>
    </div>
  </div>
</template>

<script>
import ArticleButton from "./ArticleButton.vue";

export default {
  name: "article-list",
  components: {
    ArticleButton,
  },
  props: {
    articleList: {
      type: Array,
    },
  },
};
</script>

<style scoped lang="scss">
.container {
  height: max-content;
  background-color: #fff;
  border-radius: 4px;
}
.article-list__item {
  width: 100%;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px;
  cursor: pointer;
}
.article-list__item:not(:last-child) {
  border-bottom: 2px solid #f5faff;
}
</style>
