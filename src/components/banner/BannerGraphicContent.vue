<template>
  <div>
    <img :src="imageUrl" alt="random photo">
    {{ randomColor }}
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
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
