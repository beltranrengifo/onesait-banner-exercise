<template>
  <section
    class="banner"
  >
    <div
      class="banner__wrap"
    >
      <banner-text-content />
      <banner-graphic-content />
    </div>
  </section>
</template>

<script>
import BannerTextContent from '@/components/banner/BannerTextContent'
import BannerGraphicContent from '@/components/banner/BannerGraphicContent'

export default {
  name: 'Banner',
  components: {
    BannerTextContent,
    BannerGraphicContent
  }
}
</script>

<style lang="scss" scoped>
  .banner {
    &,
    * {
      box-sizing: border-box;
    }
    &__wrap {
      width: 1200px;
      max-width: 100%;
      padding: 24px;
      margin: 0 auto;
      min-height: 100vh;
    }
  }
</style>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Titillium+Web&display=swap');
  @import url('https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.min.css');
  html {
    font-family: 'Titillium Web', sans-serif;
  }
</style>
