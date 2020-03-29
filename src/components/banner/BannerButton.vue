<template>
  <div class="button__wrap">
    <button
      class="button__button"
      @click="handleClick"
    >
      {{ text }}
    </button>
  </div>
</template>

<script>
export default {
  name: 'BannerButton',

  props: {
    text: {
      type: String,
      required: true
    }
  },

  methods: {
    handleClick () {
      this.$emit('buttonClick')
    }
  }

}
</script>

<style lang="scss" scoped>
.button {
  &__button {
    background: var(--color-primary);
    color: var(--color-white);
    font-family: var(--main-font);
    padding: 12px 32px;
    font-size: 1rem;
    font-weight: 300;
    letter-spacing: 1px;
    cursor: pointer;
    transition: var(--default-transition);
    &:focus {
      outline: var(--color-primary) auto 1px;
    }
    &:hover {
      opacity: .8;
    }
  }
}
</style>
