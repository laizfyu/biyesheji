<template>
  <view>
    <view style="height: 120rpx;">
      <view class="addShouna" @click="getAddwupin">
        <image src="../../static/iconfont/add_shouna.png" mode=""></image>
        <text>新增收纳</text>
      </view>
    </view>
    <view class="shouna_center">
      
      <view class="shouna_item" @click="getWupin">
        <view class="item_head">
          <view class="head_lf">
            <image src="../../static/iconfont/add_item.png" mode=""></image>
            <text>XF0001</text>
          </view>
          <text class="head_rt">饮料</text>
        </view>
        <view class="item_center">
          <image src="../../static/img/pic_add.png" mode="aspectFit"></image>
          <view class="center_show"><text>描述:</text>编译成功。前端运行日志，请另行在小程序开发工具的控制台查看。编译成功。前端运行日志，请另行在小程序开发工具的控制台查看编译成功。前端运行日志，请另行在小程序开发工具的控制台查看</view>
        </view>
        <view class="item_bottom">
          <view>2021/12/09</view>
          <view><text>¥ 5</text> <text>x 2</text></view>
        </view>
      </view>
      
    </view>
  </view>
</template>

<script>
  const app = getApp()
  const domain = app.globalData.domain
  export default {
    data() {
      return {

      }
    },
    onLoad() {

    },
    methods: {
      // 跳转到新增物品页
      getAddwupin() {
        uni.navigateTo({
          url: "../../pagesA/addwupin/addwupin"
        })
      },
      // 跳转到物品详情页
      getWupin() {
        uni.navigateTo({
          url: "../../pagesB/wupin_detail/wupin_detail"
        })
      }
    }
  }
</script>

<style lang="scss">
  .addShouna {
    width: 682rpx;
    height: 84rpx;
    background: #F5F5F5;
    border-radius: 12rpx;
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
    top: 33rpx;
    left: 50%;
    margin-left: -341rpx;

    image {
      width: 34rpx;
      height: 34rpx;
    }

    text {
      margin-left: 11rpx;
      font-size: 34rpx;
      font-family: PingFang SC;
      font-weight: 500;
      color: #282828;
    }
  }
  .shouna_center {
    .shouna_item {
     margin: 30rpx auto 0;
     padding-bottom: 20rpx;
     width: 688rpx;
     min-height: 328rpx;
     box-shadow: 0px 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.1);
     border-radius: 8rpx;
     .item_head {
       display: flex;
       justify-content: space-between;
       .head_lf {
         display: flex;
         align-items: center;
         image {
           width: 80rpx;
           height: 80rpx;
           margin-top: -10rpx;
         }
       }
       .head_rt {
         margin: 15rpx 20rpx 0 0;
       }
     }
     .item_center {
       margin: 20rpx 20rpx 0 20rpx;
       display: flex;
       flex-direction: row;
       image {
         width: 170rpx;
         height: 170rpx;
       }
       .center_show {
         width: 480rpx;
         height: 170rpx;
         // padding-top: 10rpx;
         margin-left: 12rpx;
         font-size: 25rpx;
         color: #8c8c8c;
         display: -webkit-box;
         -webkit-box-orient: vertical;
         -webkit-line-clamp: 4;
         overflow: hidden;
         text {
           font-size: 30rpx;
           font-weight: 500;
           color: #000000;
         }
       }
     }
     .item_bottom {
       display: flex;
       justify-content: space-between;
       padding: 0 20rpx;
       margin-top: 20rpx;
       text {
         margin-right: 10rpx;
       }
     }
    }
  }
</style>
