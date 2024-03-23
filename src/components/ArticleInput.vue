<template>
  <div class="article-input__container">
    <label class="text--medium font--sm main-grey">
      <slot name="label"></slot>
    </label>
    <div>
      <input
        min="0"
        :type="type"
        :placeholder="placeholder"
        :class="`${inputClass} ${hasIcon ? 'article-input-icon__input' : ''}`"
        :value="value"
        @input="updateValue($event.target.value)"
      />
      <div v-if="hasIcon" class="article-input-icon__icon">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "article-input",
  props: {
    value: {},
    type: {
      type: String,
      default: "text",
      validator: (value) => {
        return [
          "button",
          "checkbox",
          "color",
          "date",
          "datetime-local",
          "email",
          "file",
          "hidden",
          "image",
          "month",
          "number",
          "password",
          "radio",
          "range",
          "reset",
          "search",
          "submit",
          "tel",
          "text",
          "time",
          "url",
          "week",
        ].includes(value);
      },
    },
    placeholder: {
      type: String,
    },
    inputClass: {
      type: String,
    },
    hasIcon: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    updateValue(newValue) {
      this.$emit("input", newValue);
    },
  },
};
</script>

<style scoped lang="scss">
.article-input__text {
  height: 50px;
  width: 100%;
  padding: 12px;
  border: 2px solid #d5dde5;
  border-radius: 8px;
}
.article-input__text::placeholder {
  color: #d5dde5;
  opacity: 1;
}
.article-input__container {
  margin-top: 16px;
  position: relative;
  width: 100%;
}
.article-input__container > label {
  padding-left: 5px;
  padding-right: 5px;
  position: absolute;
  top: -6px;
  left: 20px;
  background-color: white;
}
.article-input__container > input {
  border: none;
  height: 50px;
  width: 100%;
  padding: 12px;
  border: 2px solid #d5dde5;
  border-radius: 8px;
}
.article-input-icon__input {
  width: 100%;
  text-align: right;
  padding-right: 38px;
}
.article-input-icon__icon {
  height: 46px;
  width: 30px;
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
  background-color: #f5faff;
  position: absolute;
  right: 2px;
  top: 2px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
