<template>
  <div class="container">
    <form @submit.prevent="save">
      <div
        style="
          display: flex;
          align-items: center;
          justify-content: space-between;
          margin-bottom: 16px;
        "
      >
        <h1 class="text--demibold font--lg main-dark">
          {{ isNew ? "Ajouter un article" : "Éditer un article" }}
        </h1>
        <i
          class="fas fa-xmark fa-lg close-edit__icon"
          style="cursor: pointer"
          @click="$emit('onCloseEdit')"
        ></i>
      </div>
      <ArticleInput
        :value="localValue.name"
        placeholder="Nom de l'article"
        input-class="text--medium font--md main-light article-input__text"
        @input="localValue.name = $event"
      />
      <ArticleInput
        :value="localValue.price"
        :has-icon="true"
        placeholder="50"
        type="number"
        input-class="text--medium font--md main-light article-input__text"
        @input="localValue.price = $event"
      >
        <template #label> Prix unitaire HT </template>
        <template #default> € </template>
      </ArticleInput>
      <ArticleInput
        :value="localValue.vat"
        :has-icon="true"
        placeholder="20"
        type="number"
        input-class="text--medium font--md main-light article-input__text"
        @input="localValue.vat = $event"
      >
        <template #label> TVA en % </template>
        <template #default> % </template>
      </ArticleInput>
      <div
        style="display: flex; justify-content: space-between; margin-top: 24px"
      >
        <span class="text--medium font--md main-dark">Prix total TTC</span>
        <span class="text--medium font--md main-dark">{{ totalPrice }} €</span>
      </div>
      <div class="button-group__container">
        <ArticleButton :disabled="disabled" type="submit">
          Enregistrer l'article
        </ArticleButton>
        <ArticleButton
          color="error"
          style="margin-top: 16px"
          :disabled="isNew"
          @onClick="$emit('onDeleteArticle')"
        >
          Supprimer l'article
        </ArticleButton>
      </div>
    </form>
  </div>
</template>

<script>
import ArticleInput from "./ArticleInput.vue";
import ArticleButton from "./ArticleButton.vue";

export default {
  name: "article-write",
  components: { ArticleInput, ArticleButton },
  props: {
    selected: {
      type: Object,
    },
    isNew: {
      type: Boolean,
    },
  },
  data() {
    return {
      localValue: {},
    };
  },
  computed: {
    totalPrice() {
      if (this.localValue.price) {
        let vatRate = parseFloat(this.localValue.vat);
        if (vatRate) {
          let priceIncludingVAT = this.localValue.price * (1 + vatRate / 100);
          return priceIncludingVAT.toFixed(2).replace(".", ",");
        } else {
          return "-";
        }
      }
      return "0,00";
    },
    disabled() {
      return (
        !this.localValue.name ||
        !this.localValue.price ||
        !this.localValue.vat ||
        this.totalPrice === "-"
      );
    },
  },
  watch: {
    selected: {
      immediate: true,
      deep: true,
      handler(newVal, oldVal) {
        if (!oldVal || JSON.stringify(newVal) !== JSON.stringify(oldVal)) {
          this.localValue = JSON.parse(JSON.stringify(newVal));
        }
      },
    },
  },
  methods: {
    save() {
      this.localValue.priceIncludingVAT = this.totalPrice.replace(",", ".");
      this.$emit("onSave", JSON.parse(JSON.stringify(this.localValue)));
    },
  },
};
</script>

<style scoped lang="scss">
.container {
  height: max-content;
  position: sticky;
  top: 8px;
  background-color: #fff;
  padding: 16px;
  border-radius: 4px;
}
.button-group__container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 40px 0 24px 0;
}
</style>
