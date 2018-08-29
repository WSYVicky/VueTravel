<template>
  <div>
    <div class="item" v-for="(item, index) of list" :key="index">
      <div class="item-title border-bottom">
        <span class="item-title-icon"></span>
        {{item.title}}
      </div>
      <!--递归组件-->
        <!--如果item存在list-->
      <div v-if="item.children" class="item-children">
        <detail-list :list="item.children"></detail-list>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DetailList',
  props: {
    list: Array
  }
}
</script>

<style lang="stylus" scoped>
  .item-title
    line-height .8rem
    height .8rem
    padding: .2rem
    font-size .32rem
    text-align left
    .item-title-icon
      display inline-block
      position: relative
      width: .36rem
      height: .36rem
      top: .06rem
      left: .06rem
      background: url(http://s.qunarzz.com/piao/image/touch/sight/detail.png) 0 -.45rem no-repeat
      margin-right: .1rem;
      background-size: .4rem 3rem;
  .item-children
    padding: .2rem
</style>
