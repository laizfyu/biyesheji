<template>
  <view>
    <view class="personal_data">
      <view class="name">
        <view>姓 名：</view>
        <view>{{users.userName}}</view>
      </view>
      <view class="line"></view>
      <view class="number">
        <view>电话号码：</view>
        <view>{{users.userPhone}}</view>
      </view>
      <view class="line"></view>
    </view>
    <view class="btn" @click="outLogin">
      退出登录
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        users: ""
      }
    },
    onShow() {
      this.users = uni.getStorageSync("userInfo");
    },
    methods: {
      outLogin() {
        wx.removeStorageSync("userInfo");
        wx.reLaunch({
          url: "/pages/index/index"
        })
      }
    }
  }
</script>

<style lang="scss">
  page {
    background-color: #F0F4F7;
  }

  .line {
    // width: 510rpx;
    height: 4rpx;
    background: #F1F3F4;
    margin-top: 30rpx;
    margin-left: 74rpx;
    margin-bottom: 30rpx;
  }

  .personal_data {
    margin: 50rpx;
    background-color: #FFFFFF;
    padding: 30rpx;

    .name {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .number {
      display: flex;
      justify-content: space-between;
      align-items: center;

      .pic {
        color: #007AFF;
      }
    }
  }
  .btn {
    width: 110rpx;
    margin: 200rpx auto;
    color: red;
  }
</style>
