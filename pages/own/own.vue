<template>
  <view>
    <view class="own_head">
      <view class="head_lf">
        <image :src="imgurl" @click="getImg()"></image>
        <view class="lf_rt">
          <open-data type="userNickName"></open-data>
          <text>108814</text>
        </view>
      </view>
      <view class="head_rt" @click="getmember()">
        <image src="../../static/iconfont/xiugai@2x.png" mode=""></image>
      </view>
    </view>
    <view class="own_center">
      
      <view class="center_jilu" @click="getFamily()">
        <view>
          <image src="../../static/iconfont/family.png" class="center_img"></image>
          <text>家庭管理</text>
        </view>
        <view>
          <image src="../../static/iconfont/arrow-right.png" mode=""></image>
        </view>
      </view>
      
      <view class="center_jilu" @click="getBox()">
        <view>
          <image src="../../static/iconfont/box.png" class="center_img"></image>
          <text>盒子管理</text>
        </view>
        <view>
          <image src="../../static/iconfont/arrow-right.png" mode=""></image>
        </view>
      </view>
    
    <view class="center_jilu" @click="getPhone()">
        <view>
          <image src="../../static/iconfont/phone.png" class="center_img"></image>
          <text>电话号码</text>
        </view>
        <view>
          <image src="../../static/iconfont/arrow-right.png" mode=""></image>
        </view>
      </view>
    </view>
    
    <view class="login_box">
      <view v-if="isLogin" class="btn login" @click="goLogin">登录</view>
      <view v-else class="btn out_login" @click="outLogin">退出登录</view>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        imgurl: "../../static/img/touxiang.jpg",
        isLogin: true,
        openId: "",
        userInfo: ""
      }
    },
    onShow() {
      console.log(uni.getStorageSync("token"));
      if (uni.getStorageSync("token")) {
        this.isLogin = false;
        this.openId = uni.getStorageSync("openId");
        this.getUserInfo();
      } else {
        this.isLogin = true;
      }
    },
    methods: {
      // 跳转到个人信息页
      getmember() {
        uni.navigateTo({
          url: "../../pagesA/member/member"
        })
      },
      // 跳转到家庭页面
      getFamily() {
        uni.navigateTo({
          url: "../../pagesA/family/family"
        })
      },
      // 跳转到盒子管理页面
      getBox() {
        uni.navigateTo({
          url: "../../pagesA/box/box"
        })
      },
      getPhone() {
        uni.navigateTo({
          url: "../../pagesA/xinxi/phone/phone"
        })
      },
      // 跳转到登录页面
      goLogin() {
        this.$login
          // .checkLogin()
          // .then(() => {
          //   // 已登录
          //   console.log("已登录");
          // })
          // .catch(() => {
          //   // 未登录
          //   console.log("未登录");
            wx.reLaunch({
              url: "/pages/login/login",
            });
          
      },
      // 退出登录
      outLogin() {
        this.$login.exitLogin();
      },
    }
  }
</script>

<style lang="scss">
  .own_head {
    width: 100%;
    height: 220rpx;
    border-bottom: 9px solid #f5f5f5;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    .head_lf {  
      margin-top: 20rpx;
      margin-left: 37rpx;
      display: flex;
      flex-direction: row;
      align-items: center;
      image {
        width: 147rpx;
        height: 147rpx;
        border-radius: 50%;
      }
      .lf_rt {
        display: flex;
        flex-direction: column;
        margin-left: 20rpx;
        font-size: 40rpx;
        font-family: PingFang SC;
        font-weight: 500;
        color: #333333;
        text {
          font-size: 30rpx;
          font-family: PingFang SC;
          font-weight: 500;
          color: #333333;
          margin-top: 20rpx;
        }
      }
    }

    .head_rt {
      image {
        width: 40rpx;
        height: 40rpx;
        margin-right: 30rpx;
      }
    }
  }

  .own_center {
    .center_jilu {
      width: 100%;
      height: 90rpx;
      line-height: 90rpx;
      border-bottom: 2rpx solid #E4E4E4;
      padding-left: 40rpx;
      padding-right: 20rpx;
      display: flex;
      justify-content: space-between;

      view {
        image {
          width: 24rpx;
          height: 24rpx;
        }
      }

      .center_img {
        float: left;
        width: 48rpx;
        height: 48rpx;
        margin-top: 22rpx;
        margin-right: 10rpx;
      }
    }
  }

  .login_box {
    .btn {
      width: 688rpx;
      height: 80rpx;
      border-radius: 12rpx;
      line-height: 80rpx;
      text-align: center;
      margin: 230rpx auto;
      background-color: #fff;
    }

    .login {
      color: #269e3a;
    }

    .out_login {
      color: red;
    }
  }
</style>
