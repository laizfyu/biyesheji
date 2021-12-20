<template>
  <view>
    <!-- 用户头像 -->
    <view class="member_center" @click="gettouxiang()">
      <view class="headImg">
        <view><text>头像</text></view>
        <view style="float: left; margin-top: 5rpx; margin-left: 5rpx;">
          <image :src="img" mode="" style="width: 80rpx; height: 80rpx;"></image>
        </view>
      </view>
      <view>
        <image src="../../static/iconfont/arrow-right.png" mode=""></image>
      </view>
    </view>
    <!-- 用户名字 -->
    <view class="member_center" @click="getName()">
      <view>
        <text>用户名</text>
      </view>
      <view>
        <text>Laizf</text>
      </view>
    </view>
    <!-- 用户电话 -->
  <!--  <view class="member_center" @click="getPhone">
      <view>
        <text>绑定电话号码</text>
      </view>
      <view>
        <image src="../../static/iconfont/arrow-right.png" mode=""></image>
      </view>
    </view> -->
    <!-- 用户性别 -->
    <view class="member_center">
      <view>
        <text>性别</text>
      </view>
      <view>
        <u-radio-group v-model="value" @change="sexChange" active-color="#dfa46c">
          <u-radio 
          v-for="(item,index) in list" 
          :key="index"
          :name="item.name">
          {{item.name}}
          </u-radio>
        </u-radio-group>
      </view>
    </view>

    <view class="member_button">
      <u-button type="warning" shape="circle" size="medium">保存</u-button>
      <u-button shape="circle" size="medium">取消</u-button>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        img: "../../static/img/touxiang.jpg",
        value: "男",
        list: [{
          name: "男"
        }, {
          name: "女"
        }]
      }
    },
    methods: {
      gettouxiang() {
        uni.navigateTo({
          url: "../xinxi/touxiang/touxiang"
        })
      },
      getName() {
        uni.navigateTo({
          url: "../xinxi/name/name"
        })
      },
      // getPhone() {
      //   uni.navigateTo({
      //     url: "../xinxi/phone/phone"
      //   })
      // },
      // getPassword() {
      //   uni.navigateTo({
      //     url: "../xinxi/password/password"
      //   })
      // },
      // getSex() {
      //   uni.navigateTo({
      //     url: "../xinxi/sex/sex"
      //   })
      // }
    }
  }
</script>

<style lang="scss">
  .member_center {
    width: 100%;
    height: 90rpx;
    line-height: 90rpx;
    border-bottom: 2rpx solid #E4E4E4;
    padding-left: 40rpx;
    padding-right: 20rpx;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .headImg {
      display: flex;
      flex-wrap: nowrap;
    }

    view {
      image {
        width: 24rpx;
        height: 24rpx;
      }
    }
  }

  .member_button {
    display: flex;
    justify-content: space-around;
    margin-top: 80rpx;
  }
</style>
