<template>
  <div class="article-page__container">
    <ArticleList
      :class="closeEdit ? '' : 'hide-section'"
      :article-list="articleList"
      @onEditArticle="
        selectedArticleIndex = $event;
        closeEdit = false;
      "
      @onAddArticle="
        selectedArticleIndex = null;
        closeEdit = false;
      "
    />
    <ArticleWrite
      :class="closeEdit ? 'hide-section' : ''"
      :selected="selectedArticle"
      :is-new="selectedArticleIndex === null"
      @onSave="
        selectedArticleIndex === null ? addArticle($event) : saveArticle($event)
      "
      @onDeleteArticle="deleteArticle"
      @onCloseEdit="closeEdit = true"
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
      closeEdit: false,
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
      this.closeEdit = true;
    },
    addArticle(value) {
      this.articleList.push(value);
      this.selectedArticleIndex = this.articleList.length - 1;
      this.closeEdit = true;
    },
    deleteArticle() {
      if (
        confirm(
          "Vous êtes sur le point de supprimer cet article. Êtes-vous sûr de vouloir continuer ?"
        )
      ) {
        this.articleList.splice(this.selectedArticleIndex, 1);
        this.selectedArticleIndex = null;
        this.closeEdit = true;
      }
    },
  },
};
</script>
