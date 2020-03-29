<template>
  <div
    class="graphic-content__wrap"
    :class="{
      'invert': invert,
      'grid': grid
    }"
  >
    <img
      class="graphic-content__image"
      :src="imageUrl"
      alt="random photo">
    <div
      class="graphic-content__tile"
      :style="tileStyles"/>
  </div>
</template>

<script>

export default {
  name: 'BannerGraphicContent',

  props: {
    imageUrl: {
      type: String,
      required: true
    },
    randomColor: {
      type: String,
      default: '#b1cfe5'
    },
    invert: {
      type: Boolean,
      default: false
    },
    grid: {
      type: Boolean,
      default: false
    }
  },

  computed: {
    tileStyles () {
      return {
        'background-color': this.randomColor
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.graphic-content {
  $--self: &;
  &__wrap {
    position: relative;
    padding: 3rem 0 3rem 3.5rem;
    transition: var(--default-transition);
    &.invert {
      padding: 3rem 3.5rem 3rem 0;
      #{$--self}__tile {
        left: calc(100% - 175px);
      }
      &.grid {
        order: -1;
      }
    }
  }
  &__image {
    position: relative;
    z-index: 2;
  }
  &__tile {
    position: absolute;
    bottom: 0;
    left: 0;
    height: 155px;
    width: 175px;
    z-index: 1;
    transition: var(--default-transition);
  }
}
</style>
