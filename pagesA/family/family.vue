<template>
  <view>
    <view class="familyItem">
      <view class="news_head">
        <view class="head_lf">
          <image src="../../static/iconfont/family_item.png" mode=""></image> 
          <view class="bkg"><text>FY0001</text></view>
        </view>
        <image src="../../static/iconfont/arrow-right.png" mode="" @click="getFamily"></image>
      </view>
      <view class="news_center">
        <image src="../../static/img/pic_add.png" mode="aspectFit"></image>
        <view class="familyNews">
          <image src="../../static/iconfont/item.png" mode=""></image>
          <view>成员: {{number}}</view>
        </view>
      </view>
      <view class="news_bottom">
        <view>2021/12/21</view>
        <view>小明的一家人</view>
      </view>
    </view>
    <button type="default" class="buttom" @click="addFamily">组建家庭</button>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        number: 5
      }
    },
    methods: {
      getFamily() {
        uni.navigateTo({
          url: "../../pagesB/family_detail/family_detail"
        })
      },
      addFamily() {
        uni.navigateTo({
          url: "../../pagesB/addFamily/addFamily"
        })
      }
    }
  }
</script>

<style lang="scss">
  .familyItem {
    width: 688rpx;
    min-height: 300rpx;
    background: #ffffff;
    box-shadow: 0rpx 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.05);
    border-radius: 8rpx;
    margin: 27rpx auto 0;
    padding: 20rpx;
    .news_head {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 30rpx;
      font-family: PingFang SC;
      font-weight: 500;
      color: #2C2C2C;
      .head_lf {
        display: flex;
        flex-direction: row;
        align-items: center;
        .bkg {
          // background-image: url(../../static/iconfont/tips@2x%20.png);
          // background-size: cover;
          // background-repeat: no-repeat;
          // width: 120rpx;
          // height: 50rpx;
          line-height: 50rpx;
          text {
            margin-left: 10rpx;
          }
        }
      }
      image {
        width: 50rpx;
        height: 50rpx;
      }
    }
    .news_center {
      margin-top: 10rpx;
      display: flex;
      flex-direction: row;
      align-items: flex-start;
      image {
        width: 250rpx;
        height: 200rpx;
      }
      .familyNews {
        margin-left: 20rpx;
        color: #d19a66;
        display: flex;
        flex-direction: row;
        align-items: flex-end;
        image {
          width: 50rpx;
          height: 50rpx;
          margin-right: 10rpx;
        }
      }
    }
    .news_bottom {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10rpx;
      color: #efa856;
      font-size: 30rpx;
    }
  }
  .buttom {
    width: 640rpx;
    height: 84rpx;
    position: fixed;
    bottom: 20rpx;
    left: 50%;
    margin-left: -320rpx;
    background-color: #e19d3e !important;
  }
</style>
