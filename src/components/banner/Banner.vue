<template>
  <section
    :key="key"
    class="banner"
  >
    <div
      class="banner__wrap"
      :class="{
        'banner__wrap--flex': useFlex,
        'banner__wrap--grid': !useFlex,
        'inverted': invertLayoutOrder
      }"
    >
      <banner-text-content
        :label="label"
        :title="title"
        :subtitle="subtitle"
        :invert="invertLayoutOrder"
        @handleButton="refreshContent"
      />
      <banner-graphic-content
        :image-url="imageUrl"
        :random-color="randomColor"
        :invert="invertLayoutOrder"
        :grid="!useFlex"
      />
    </div>
  </section>
</template>

<script>
import axios from 'axios'
import { EventBus } from './event-bus'
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
      subtitle: '',
      useFlex: true,
      invertLayoutOrder: false,
      key: 0
    }
  },

  computed: {
    imageUrl () {
      return 'https://picsum.photos/1160/780'
    },

    randomColor () {
      return colors[Math.floor(Math.random() * colors.length)]
    }
  },

  created () {
    this.getTextContent()
    EventBus.$on('invertLayout', this.invertLayout)
    EventBus.$on('switchType', this.switchType)
  },

  methods: {
    async getTextContent () {
      const { data } = await axios.get('https://baconipsum.com/api/?type=meat-and-filler&paras=1')
      const text = data[0].toLowerCase().replace(/\. |,/g, '')
      this.title = this.getChunk(text, 0, 11)
      this.label = this.getChunk(text, 11, 46)
      this.subtitle = this.getChunk(text, 32, 135)
    },

    getChunk (text, a, b) {
      return text.substring(a, b).trim()
    },

    invertLayout () {
      this.invertLayoutOrder = !this.invertLayoutOrder
    },

    switchType () {
      this.useFlex = !this.useFlex
    },

    refreshContent () {
      this.key++
      this.getTextContent()
    }
  }
}
</script>

<style lang="scss" scoped>
  @import 'breakpoints.scss';

  .banner {
    &,
    * {
      box-sizing: border-box;
    }

    &__wrap {
      width: var(--main-width);
      max-width: 100%;
      padding: 24px;
      margin: 0 auto;

      &--flex {
        display: flex;
        align-items: center;
        flex-direction: row;

        & > * {
          flex: 0 0 50%;
          @include for-size(until-tablet) {
            width: 100%;
          }
        }
        &.inverted {
          flex-direction: row-reverse;
          transition: var(--default-transition);
          @include for-size(until-tablet) {
            flex-direction: column-reverse;
          }
        }

        @include for-size(until-tablet) {
          flex-direction: column;
        }
      }

      &--grid {
        display: grid;
        grid-template-columns: repeat(2, 50%);
        align-items: center;

        @include for-size(until-tablet) {
          grid-template-columns: repeat(1, 100%);
        }
      }
    }
  }
</style>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Titillium+Web:300,400,600&display=swap');
  @import url('https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.min.css');

  :root {
    --color-main: #193b47;
    --color-green: #79c5b4;
    --color-primary: #2e6c99;
    --color-secondary: #87BEE6;
    --color-grey: #D5DCE0;
    --color-grey-dark: #6E767D;
    --color-white: white;
    --main-width: 1360px;
    --main-font: 'Titillium Web', sans-serif;
    --default-transition: .3s all ease-out;
  }

  html {
    font-family: var(--main-font);
    font-weight: 300;
    color: var(--main-color);
    font-size: 16px;
  }

  img {
    max-width: 100%;
  }
</style>
