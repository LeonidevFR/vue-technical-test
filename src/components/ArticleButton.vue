<template>
  <button
    class="text--medium font--md"
    :class="`${color}__button ${rounded ? 'rounded' : ''}`"
    :disabled="disabled"
    @click="$emit('onClick')"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "article-button",
  props: {
    color: {
      type: String,
      default: "primary",
    },
    rounded: {
      type: Boolean,
      default: false,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style scoped lang="scss">
.button__base {
  height: 40px;
  width: max-content;
  padding: 0 20px;
  border-radius: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  cursor: pointer;
}
.primary__button {
  @extend .button__base;
  background-color: #ff916f;

  &:hover {
    background-color: #cf6c4e;
  }

  &:disabled {
    background-color: #ffe0d6;
    cursor: not-allowed;
  }
}
.error__button {
  @extend .button__base;
  background-color: #fe5050;

  &:hover {
    background-color: #dc3d3d;
  }

  &:disabled {
    background-color: #ffd7d7;
    cursor: not-allowed;
  }
}
.rounded {
  height: 40px;
  width: 40px;
}
</style>
