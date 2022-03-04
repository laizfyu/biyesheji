<template>
  <view>
    <view class="box_item" v-for="(item,index) in boxList" :key="item.index" @click="getDetail(index)">
      <view class="box_head">
        <view class="head_lf">
          <text>{{item.boxId}}</text>
        </view>
        <view>{{item.boxName}}</view>
      </view>
      <view class="box_center">
        <view class="center_lf">
          <image :src="item.boxImg" mode="aspectFit"></image>
        </view>
        <view class="center_rt">
          <text>盒子位置:</text>
          {{item.boxMiaoshu}}
        </view>
      </view>
    </view>
    
    <!-- <view class="box_item" @click="getDetail">
      <view class="box_head">
        <view class="head_lf">
          <text>BX0003</text>
        </view>
        <view>小华的鞋柜</view>
      </view>
      <view class="box_center">
        <view class="center_lf"><image src="https://img1.baidu.com/it/u=3752411243,940585547&fm=26&fmt=auto" mode="aspectFit"></image></view>
        <view class="center_rt">
          <text>盒子位置:</text>
          项目 'receive' 编译成功。前端运行日志，请另行在小程序开发工具的控制台查看。
          项目 'receive' 编译成功。前端运行日志，请另行在小程序开发工具的控制台查看。
          项目 'receive' 编译成功。前端运行日志，请另行在小程序开发工具的控制台查看。
        </view>
      </view>
    </view> -->
    <!-- 底部新增按钮 -->
    <view class="addBox" @click="getAddbox()">
      <image src="../../static/iconfont/add_shouna.png" mode=""></image>
      <text>新增收纳盒子</text>
    </view>
  </view>
</template>

<script>
  const app = getApp()
  const domain = app.globalData.domain
  export default {
    data() {
      return {
        user_id: "", //用户openid
        boxList: "",
        Img: ""
      }
    },
    onShow() {
      this.getBoxList()
    },
    methods: {
      getBoxList() {
        const users = uni.getStorageSync("userInfo");
        console.log("用户信息:")
        console.log(users);
        this.user_id = users.userId;
        wx.request({
          url: domain + "/boxList",
          method: "POST" ,
          data: {
            userId: this.user_id,
          },
          success:(res) => {
            // console.log(res)
            this.boxList = res.data.data;
            console.log(this.boxList)
          }
        })
      },
      getAddbox() {
        uni.navigateTo({
          url: "../../pagesB/addBox/addBox"
        })
      },
      getDetail(index) {
        let detail = this.boxList[index];
        uni.navigateTo({
          url: "/pagesB/box_detail/box_detail?detail=" + encodeURIComponent(JSON.stringify(detail)),
        })
      }
    }
  }
</script>

<style lang="scss">
  .box_item {
    width: 696rpx;
    height: 256rpx;
    margin: 30rpx auto;
    padding-top: 26rpx;
    background: #FFFFFF;
    box-shadow: 0px 2rpx 6rpx 0rpx rgba(86, 86, 86, 0.13);
    border-radius: 24rpx;

    .box_head {
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-right: 20rpx;
      .head_lf {
        background-image: url(../../static/iconfont/tips@2x%20.png);
        background-size: cover;
        background-repeat: no-repeat;
        width: 120rpx;
        height: 50rpx;
        line-height: 50rpx;

        text {
          margin-left: 10rpx;
        }
      }

    }

    .box_center {
      margin: 20rpx;
      display: flex;
      flex-direction: row;
      align-items: center;
      .center_lf {
        image {
          width: 130rpx;
          height: 130rpx;
        }
      }
      .center_rt {
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 4;
        -webkit-box-orient: vertical;
        margin-left: 20rpx;
        text {
          font-size: 30rpx;
          font-weight: 500;
          margin-right: 10rpx;
        }
      }
    }
  }
  .addBox {
    width: 682rpx;
    height: 84rpx;
    background: #F5F5F5;
    border-radius: 12rpx;
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
    bottom: 33rpx;
    left: 50%;
    margin-left: -341rpx;
    z-index: 999;
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
</style>
