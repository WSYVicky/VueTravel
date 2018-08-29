<template>
  <div>
    <div class="banner" @click="handleBannerClick">
      <img class="banner-img" :src="bannerImg" />
      <div class="banner-info">
        <div class="banner-title">{{this.sightName}}</div>
        <div class="banner-number">
          <span class="iconfont banner-icon">&#xe600;</span>
          {{this.bannerImgs.length}}
        </div>
      </div>
    </div>
    <fade-animation>
      <common-gallary :imgs="bannerImgs" v-show="showGallary"  @close="handleBannerClose"></common-gallary>
    </fade-animation>
  </div>
</template>

<script>
import CommonGallary from 'common/gallary/Gallary'
import FadeAnimation from 'common/fade/FadeAnimation'
export default {
  name: 'Banner',
  props: {
    sightName: String,
    bannerImg: String,
    bannerImgs: Array
  },
  data () {
    return {
      showGallary: false
    }
  },
  methods: {
    handleBannerClick () {
      this.showGallary = true
    },
    handleBannerClose () {
      this.showGallary = false
    }
  },
  components: {
    CommonGallary,
    FadeAnimation
  }
}
</script>

<style lang="stylus" scoped>
  .banner
    overflow hidden
    position relative
    height 0
    padding-bottom 55%
    .banner-img
      width 100%
    .banner-info
      display flex
      position absolute
      right: 0
      left: 0
      bottom: 0
      text-align left
      float left
      color: #fff
      line-height .6rem
      background-image : linear-gradient(top, rgba(0,0,0, 0),rgba(0,0,0, .8))
      .banner-title
        flex: 1
        padding 0 .2rem
        font-size .36rem
        font-weight bolder
        text-shadow: 0 1px 2px rgba(0,0,0,0.70)
      .banner-number
        width 1.0rem
        background rgba(0,0,0, .5)
        font-size: .30rem
        padding .09rem .2rem
        line-height .3rem
        height: .3rem
        border-radius .2rem
        text-align center
        margin-top .08rem
        .banner-icon
          font-size: .32rem
</style>
