<template>
  <view class="search">
    <u-search 
    placeholder="输入分类 便签 位置 名称进行检索" 
    v-model="keyword"
    shape="round"
    :clearabled="true">
    </u-search>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        keyword: ''
      }
    },
    methods: {
      
    }
  }
</script>

<style lang="scss">
.search {
  width: 688rpx;
  margin: 20rpx auto;
}
</style>
