<template>
  <div>
    <v-header :seller='seller'></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <a v-link="{path: '/goods'}">商品</a>
      </div>
      <div class="tab-item">
        <a v-link="{path: '/ratings'}">评论</a>
      </div>
      <div class="tab-item">
        <a v-link="{path: '/seller'}">商家</a>
      </div>
    </div>
    <router-view>
      
    </router-view>
  </div>
</template>

<script>
import vHeader from './components/header/header'
export default {
  data () {
    return {
      seller: {}
    }
  },
  created () {
    this.$http.get('/api/seller').then((res) => {
      if (res.body.errno === 0) {
        this.seller = res.body.data
        console.log(this.seller)
      }
    })
  },
  components: {
    vHeader
  }
}
</script>

<style lang="scss" scoped>
@import './common/css/mixin.scss';
.tab {
  display: flex;
  height: 40px;
  line-height: 40px;
  border-top: 1px solid rgba(7, 17, 27, .1);
  @include border-1px(rgba(7, 17, 27, .1));
  .tab-item {
    flex: 1;
    text-align: center;
    & > a {
      display: block;
      font-size: 14px;
      color: rgb(77, 85, 93);
      &.active {
        color: rgb(240, 20, 20);
      }
    }
  }
}
</style>