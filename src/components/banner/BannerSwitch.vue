<template>
  <div class="switch__wrap">
    <span class="switch__label">{{ disabledText }}</span>
    <div
      class="switch__inner"
      :class="{ 'active': value }"
      @click="handleClick"
    >
      <span
        v-if="!hideInnerText"
        class="switch__inner-text">
        On
      </span>
      <span class="switch__ball"/>
      <span
        v-if="!hideInnerText"
        class="switch__inner-text switch__inner-text--right">
        Off
      </span>
    </div>
    <span class="switch__label">{{ activeText }}</span>
  </div>
</template>

<script>
export default {
  name: 'BannerSwitch',

  props: {
    disabledText: {
      type: String,
      default: ''
    },
    activeText: {
      type: String,
      default: ''
    },
    hideInnerText: {
      type: Boolean,
      default: false
    }
  },

  data () {
    return {
      value: false
    }
  },

  methods: {
    handleClick () {
      this.value = !this.value
      this.$emit('handleSwitch', this.value)
    }
  }
}
</script>

<style lang="scss" scoped>
$--ball-dimension: 26px;
.switch {
  $--self: &;
  &__wrap {
    display: flex;
    align-items: center;
    width: 300px;
    max-width: 100%;
    justify-content: space-evenly;
  }
  &__label {
    font-size: .8rem;
    color: var(--color-grey-dark);
  }
  &__inner {
    width: 64px;
    height: 24px;
    position: relative;
    background-color: var(--color-grey);
    transition: var(--default-transition);
    border-radius: 20px;
    &.active {
      background-color: var(--color-secondary);
      #{$--self}__ball {
        transition: var(--default-transition);
        left: calc(100% - #{$--ball-dimension});
      }
    }
  }
  &__inner-text {
    font-size: .7rem;
    text-align: left;
    position: absolute;
    left: 6px;
    top: 6px;
    color: var(--color-white);
    &--right {
      left: initial;
      right: 6px;
      color: var(--color-main);
      opacity: .6;
    }
  }
  &__ball {
    z-index: 1;
    width: $--ball-dimension;
    height: $--ball-dimension;
    position: absolute;
    left: 0;
    top: -1px;
    cursor: pointer;
    background: var(--color-white);
    border-radius: 50%;
    box-shadow: 1px 1px 4px 0px rgba(173,173,173,1);
    transition: var(--default-transition);
  }
}
</style>
