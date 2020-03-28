<template>
  <div>
    {{ label }}<br>
    {{ title }}<br>
    {{ subtitle }}
  </div>
</template>

<script>

export default {
  name: 'BannerTextContent',
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
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
