<template>
  <view class="familyCenter">

    <view class="makeFamily" @click="makefamily()">
      <view>
        <text>创建家庭</text>
      </view>
      <view>
        <image src="../../static/iconfont/arrow-right.png" mode=""></image>
      </view>
    </view>

    <view class="makeFamily" @click="newfamily()">
      <view>
        <text>我的家庭</text>
      </view>
      <view>
        <image src="../../static/iconfont/arrow-right.png" mode=""></image>
      </view>
    </view>

  </view>
</template>

<script>
  export default {
    data() {
      return {

      }
    },
    methods: {
      makefamily() {
        uni.navigateTo({
          url: "../xinxi/makefamily/makefamily"
        })
      },
      newfamily() {
        uni.navigateTo({
          url: "../xinxi/newfamily/newfamily"
        })
      }
    }
  }
</script>

<style lang="scss">
  .makeFamily {
    width: 100%;
    height: 90rpx;
    line-height: 90rpx;
    border-bottom: 2rpx solid #E4E4E4;
    // padding-left: 40rpx;
    font-size: 14px;
    padding-right: 20rpx;
    display: flex;
    justify-content: space-between;

    view {
      image {
        width: 33rpx;
        height: 33rpx;
      }
    }
  }
</style>
