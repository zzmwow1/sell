<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease icon-remove_circle_outline" v-show="food.count > 0" @click.stop="decreaseCart"></div>
    </transition>
    <transition name="move">
      <div class="cart-count" v-show="food.count > 0">{{ food.count }}</div>
    </transition>
    <div class="cart-add icon-add_circle" @click.stop="addCart"></div>
  </div>
</template>

<script>
import Vue from 'vue'
export default {
  name: 'v-cartcontrol',
  props: {
    food: {
      type: Object
    }
  },
  data () {
    return {
    }
  },
  methods: {
    addCart(event) {
      if(!event._constructed) {
        return
      }
      if(!this.food.count) {
        Vue.set(this.food, 'count', 1)
      } else {
        this.food.count++
      }
      this.$emit('cart-add', event.target)
    },
    decreaseCart() {
      if(!event._constructed) {
        return
      }
      if(this.food.count) {
        this.food.count--
      }
    }
  }
}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size: 0
    .cart-decrease
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0,160,220)
      &.move-enter-active, &.move-leave-active
        transition: all .8s ease
      &.move-enter
        transform: translateX(24px) rotate(180deg)
      &.move-leave-active
        transform: translateX(48px) rotate(180deg)
        opacity: 0
    .cart-count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147,153,159)
      &.move-enter-active, &.move-leave-active
        transition: all .8s ease
      &.move-enter
        transform: translateX(24px) rotate(180deg)
      &.move-leave-active
        transform: translateX(24px)
        opacity: 0
    .cart-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0,160,220)
</style>
