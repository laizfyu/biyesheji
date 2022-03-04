<template>

  <view class="container">
    <view class="logo">
      <image class="logo-pic" src="../../static/img/jiaju.webp" mode="" />
    </view>
    <view class="welcome"> 欢迎来到居家收纳管理系统 </view>
    <view class="iQ">创造整洁居家环境</view>

      <button class='bottom' type='primary' open-type="getUserInfo" lang="zh_CN" @click="bindGetUserInfo()">
        授权登录
      </button>
    <!-- 提示 -->
    <u-top-tips ref="uTips"></u-top-tips>
  </view>

</template>

<script>
  const app = getApp()
  const domain = app.globalData.domain
  export default {
    data() {
      return {
        //判断小程序的API，回调，参数，组件等是否在当前版本可用。
        canIUse: wx.canIUse('button.open-type.getUserInfo'),
        isHide: false,
      }
    },

    methods: {
      bindGetUserInfo: function(e) {
        // 获取用户信息
        wx.getUserProfile({
          lang: "zh_CN",
          desc: "登录",
          success: (res) => {
            // console.log(res),
            wx.setStorageSync("userName", res.userInfo.nickName);
              wx.login({
                success: (open) => {
                  console.log(open);
                  console.log("code:" + open.code);
                  //发起网络请求,获取openid
                  wx.request({
                    url: domain + "/wxlogin",
                    data: {
                      code: open.code,
                    },
                    method: "POST",
                    success: (r) => {
                      console.log("用户的openid:" + r.data.msg);
                      wx.setStorageSync("userId", r.data.msg);
                      this.$refs.uTips.show({
                        title: "授权成功",
                        type: "success",
                        duration: "1500",
                      });
                      setTimeout(() => {
                        wx.reLaunch({
                          url: "/pagesA/xinxi/phone/phone",
                        });
                      }, 1000);
                    },
                    fail: (error) => {
                      console.log(error);
                      this.$refs.uTips.show({
                        title: "授权失败",
                        type: "error",
                        duration: "1500",
                      });
                    },
                    complete:(r) => {
                      console.log(r);
                    }
                  })

                }
              });
          },
          fail: (err) => {
            console.log(err)
          }
        })
      }
    }
  }
</script>

<style lang="scss">
.container {
  width: 750rpx;
}
.iQ {
  text-align: center;
  font-size: 24rpx;
  color: #959aa2;
}
.logo {
  width: 750rpx;
  margin-top: 164rpx;
  text-align: center;
  .logo-pic {
    border: 1rpx solid #ccc;
    height: 156rpx;
    width: 156rpx;
    border-radius: 50%;
  }
}
.welcome {
  margin-top: 76rpx;
  text-align: center;
  color: #514858;
  font-size: 36rpx;
}

  .bottom {
    border-radius: 80rpx;
    margin: 70rpx 50rpx;
    font-size: 35rpx;
  }
</style>
