<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <router-link  v-for="(item, index) in nav" :to="{path: item.path}" tag="div" class="tab-item" :key="item.index" active-class= "active">{{ item .name}}</router-link>
    </div>
    <div class="content">
      <keep-alive>
        <router-view :seller="seller"></router-view>
      </keep-alive>
    </div>
  </div>
</template>

<script>
import header from './components/header/header'
const ERR_OK = 0
export default {
  name: 'App',
  components: {
    VHeader: header
  },
  data () {
    return {
      nav: [
        {
          name: '商品',
          path: '/goods'
        },
        {
          name: '评论',
          path: '/ratings'
        },
        {
          name: '商家',
          path: '/seller'
        }
      ],
      seller: {}
    }
  },
  created() {
    this.$http.get('/api/seller').then((response) => {
      response = response.data
      if(response.errno === ERR_OK) {
        this.seller = response.data
        // console.log(this.seller)
      }
    })
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"
  #app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      border-1px(rgba(7,17,27,0.1))
      .tab-item
        flex: 1
        text-align: center
        font-size: 14px
        color: rgb(77,85,93)
      .active
        color: rgb(240,20,20)
</style>
