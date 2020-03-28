<template>
  <section
    class="banner"
  >
    <div
      class="banner__wrap"
    >
      <banner-text-content
        :label="label"
        :title="title"
        :subtitle="subtitle"
      />
      <banner-graphic-content
        :image-url="imageUrl"
        :random-color="randomColor"
      />
    </div>
  </section>
</template>

<script>
import axios from 'axios'
import BannerTextContent from '@/components/banner/BannerTextContent'
import BannerGraphicContent from '@/components/banner/BannerGraphicContent'
import colors from '@/components/banner/colors'

export default {
  name: 'Banner',

  components: {
    BannerTextContent,
    BannerGraphicContent
  },

  data () {
    return {
      label: '',
      title: '',
      subtitle: ''
    }
  },

  computed: {
    imageUrl () {
      return 'https://picsum.photos/1280/720'
    },

    randomColor () {
      return colors[Math.floor(Math.random() * colors.length)]
    }
  },

  created () {
    this.getTextContent()
    this.getGraphicContent()
  },

  methods: {
    async getTextContent () {
      const { data } = await axios.get('https://baconipsum.com/api/?type=meat-and-filler&paras=1&start-with-lorem=1')
      const text = data[0].toLowerCase().replace(/\. |,/g, '')
      this.label = this.getChunk(text, 0, 11)
      this.title = this.getChunk(text, 11, 42)
      this.subtitle = this.getChunk(text, 42, 100)
    },

    getChunk (text, a, b) {
      return text.substring(a, b).trim()
    }
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
