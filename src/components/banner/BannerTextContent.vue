<template>
  <div
    class="text-content__wrap"
    :class="{'invert': invert}"
  >
    <div class="text-content__label">
      <small>
        {{ label | capitalize }}
      </small>
      <banner-modal />
    </div>
    <h1 class="text-content__title">
      {{ title | capitalize }}
    </h1>
    <p class="text-content__subtitle">
      {{ subtitle | capitalize }}
    </p>
    <banner-button
      text="Click the button"
      @buttonClick="buttonClick"/>
  </div>
</template>

<script>
import BannerButton from '@/components/banner/BannerButton'
import BannerModal from '@/components/banner/BannerModal'
export default {
  name: 'BannerTextContent',

  components: {
    BannerButton,
    BannerModal
  },

  props: {
    label: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    subtitle: {
      type: String,
      required: true
    },
    invert: {
      type: Boolean,
      default: false
    }
  },

  filters: {
    capitalize (value) {
      return value.toString().charAt(0).toUpperCase() + value.slice(1) || ''
    }
  },

  methods: {
    buttonClick () {
      this.$emit('handleButton')
    }
  }
}
</script>

<style lang="scss" scoped>
  .text-content {
    &__wrap {
      padding: 3rem 3.5rem 3rem 0;
      transition: var(--default-transition);
      &.invert {
        padding: 3rem 0 3rem 3.5rem;
      }
    }
    &__label {
      display: flex;
      justify-content: space-between;
      font-size: 1.2rem;
      margin-bottom: 2rem;
    }
    &__title {
      font-size: 3.5rem;
      margin-bottom: 3rem;
      position: relative;
      padding: 0 0 1.5rem;
      &::after {
        content: '';
        position: absolute;
        bottom: 0;
        left: 0;
        width: 112px;
        height: 3px;
        background-color: var(--green-color);
      }
    }
    &__subtitle {
      font-size: 1.5rem;
      line-height: 2rem;
      margin-bottom: 2.5rem;
      width: 440px;
      max-width: 100%;
    }
  }
</style>
