<template>
  <div class="switch__wrap">
    <div
      class="switch__inner"
      :class="{ 'active': value }"
      @click="handleClick"
    >
      <span class="switch__ball"/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BannerSwitch',

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
  &__inner {
    width: 56px;
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
  &__ball {
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
