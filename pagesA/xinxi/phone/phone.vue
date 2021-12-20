<template>
  <view class="phone_center">
    <view>
      <u-field v-model="mobile" label="手机号" placeholder="请填写手机号">
      </u-field>
      <u-field v-model="code" label="验证码" placeholder="请填写验证码">
        <u-button size="mini" slot="right" type="success" @click="getCode">{{codeText}}</u-button>
      </u-field>
      <u-verification-code ref="uCode" @change="codeChange"></u-verification-code>
      <u-toast ref="uToast" />
    </view>
    <u-button type="success" shape="circle" size="medium" class="btn" @click="getSave">绑定</u-button>
  </view>
</template>

<script>
  const app = getApp()
  const domain = app.globalData.domain
  export default {
    data() {
      return {
        mobile: '',
        code: '',
        codeText: ''
      }
    },
    methods: {
      codeChange(text) {
        this.codeText = text;
      },
      getCode() {
        if (this.$refs.uCode.canGetCode) {
          // 将手机号传给后台
          wx.request({
            url: domain + "/sendSMS",
            data: {
              phone: this.mobile
            },
            method: "POST",
            success: (data) => {
              console.log(data)
            }
          })
          uni.showLoading({
            title: '正在获取验证码'
          })
          setTimeout(() => {
            uni.hideLoading();
            // 通知验证码组件内部开始倒计时
            this.$refs.uCode.start();
          }, 1000);
        } else {
          this.$u.toast('倒计时结束后再发送');
        }
      },
      getSave() {
        wx.request({
          url: domain + "/getSMS",
          data: {
            phone: this.mobile,
            xingxi: this.code
          },
          method: "POST",
          success: (res) => {
            console.log(res.data.msg)
            this.$refs.uToast.show({
              title: res.data.msg,
              type: 'warnin',
              position: 'top',
              back: 'true'
            });
          }
        })
      }
    }
  }
</script>

<style lang="scss">
  .phone_center {
    margin-top: 50rpx;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;

    .btn {
      margin-top: 50rpx;
    }
  }
</style>
