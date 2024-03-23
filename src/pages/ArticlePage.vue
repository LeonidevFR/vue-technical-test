<template>
  <div class="article-page__container">
    <ArticleList
      :article-list="articleList"
      @onEditArticle="selectedArticleIndex = $event"
      @onAddArticle="selectedArticleIndex = null"
    />
    <ArticleWrite
      :selected="selectedArticle"
      :is-new="selectedArticleIndex === null"
      @onSave="
        selectedArticleIndex === null ? addArticle($event) : saveArticle($event)
      "
      @onDeleteArticle="deleteArticle"
    />
  </div>
</template>

<script>
import ArticleList from "../components/ArticleList.vue";
import ArticleWrite from "../components/ArticleWrite.vue";

export default {
  name: "article-page",
  components: {
    ArticleList,
    ArticleWrite,
  },
  data() {
    return {
      selectedArticleIndex: null,
      articleList: [],
    };
  },
  computed: {
    selectedArticle() {
      return (
        this.articleList[this.selectedArticleIndex] ?? {
          name: "",
          price: "",
          vat: "",
          priceIncludingVAT: "",
        }
      );
    },
  },
  methods: {
    saveArticle(value) {
      this.$set(this.articleList, this.selectedArticleIndex, value);
    },
    addArticle(value) {
      this.articleList.push(value);
      this.selectedArticleIndex = this.articleList.length - 1;
    },
    deleteArticle() {
      if (
        confirm(
          "Vous êtes sur le point de supprimer cet article. Êtes-vous sûr de vouloir continuer ?"
        )
      ) {
        this.articleList.splice(this.selectedArticleIndex, 1);
        this.selectedArticleIndex = null;
      }
    },
  },
};
</script>

<style scoped lang="scss">
.article-page__container {
  position: relative;
  height: 100%;
  width: 100%;
  display: grid;
  grid-template-columns: 8fr 4fr;
  gap: 16px;
  padding: 8px;
}
</style>
