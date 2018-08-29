<template>
  <div>
    <ul class="list">
    <li v-bind:class="{'item':true, 'active':touchStatus}" v-for="item of letters" :key="item" :ref="item" @click="handleLetterClick" @touchstart.prevent="handleTouchStart" @touchmove="handleTouchMove" @touchend="handleTouchEnd">
      {{item}}</li>
    </ul>
    <div class="showZM" v-show="flag">{{letter}}</div>
  </div>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null,
      letter: '',
      flag: false
    }
  },
  updated () {
    this.startY = this.$refs['A'][0].offsetTop
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  // watch: {
  //   letter () {
  //     if (this.letter) {
  //       this.flag = true
  //     }
  //   }
  // },
  methods: {
    handleLetterClick (e) {
      this.$emit('change', e.target.innerText)
    },
    handleTouchStart () {
      this.touchStatus = true
      this.flag = true
    },
    handleTouchMove (e) {
      if (this.touchStatus) {
        if (this.timer) {
          clearTimeout(this.timer)
        }
        this.timer = setTimeout(() => {
          const touchY = e.touches[0].clientY - 79
          const index = Math.floor((touchY - this.startY) / 20)
          this.letter = this.letters[index]
          if (index >= 0 && index < this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        }, 16)
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
      this.flag = false
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import "~styles/varibles.styl"
  .list
    display flex
    flex-direction column
    justify-content center
    position absolute
    top: 1.58rem
    right: 0
    width: .4rem
    bottom 0
    .active
      background #eee
    .item
      text-align center
      color: $bgcolor
      line-height .4rem
  .showZM
    position absolute
    top: 6.0rem
    right: 40%
    background #eaeaea
    font-size 1.5rem
</style>
