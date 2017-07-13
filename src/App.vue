<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
       <div class="tab-item">
         <router-link to="/ratings">评论</router-link>
       </div>
        <div class="tab-item">
          <router-link to="/seller">{{seller.deliveryPrice}}商家</router-link>
        </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header.vue';
  export default{
    data() {
       return {
           seller: {}
       };
    },
    created() {
      this.$http.get('/api/seller')
        .then(function (response) {
            this.seller = response.data.data;
        }.bind(this))
        .catch(function (error) {
            console.log(error);
        });
    },
    components: {
      'v-header': header
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "common/stylus/mixin.styl";

    .tab
      display: flex
      width: 100%
      line-height: 40px
      /*border-bottom: 1px solid rgba(7,17,27,0.1)*/
      border-1px(rgba(7,17,27,0.1))
      .tab-item
        flex: 1
        text-align: center
        & > a
          display: block
          font-size: 14px
          color: rgb(77, 85, 93)
          &.active
            color: red
</style>
