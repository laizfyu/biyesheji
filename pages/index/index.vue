<template>
  <view>
    <view class="index_head">
      <image src="/static/iconfont/laba.png" mode=""></image>
      <view>合理收纳 , 整洁家庭</view>
    </view>
    <!-- 轮播图 -->
    <view class="swiper">
      <u-swiper :list="swiperList" :effect3d="true" height="350"></u-swiper>
    </view>
    <view style="height: 120rpx;">
      <view class="addShouna" @click="getAddwupin">
        <image src="../../static/iconfont/add_shouna.png" mode=""></image>
        <text>新增收纳</text>
      </view>
    </view>
    <view class="shouna_center">
      
      <view class="shouna_item" @click="getWupin" v-for="(item,index) in list" :key="item.index">
        <view class="item_head">
          <view class="head_lf">
            <image src="../../static/iconfont/add_item.png" mode=""></image>
            <text>{{item.wupinId}}</text>
          </view>
          <text class="head_rt">{{item.wupinName}}</text>
        </view>
        <view class="item_center">
          <image src="../../static/img/pic_add.png" mode="aspectFit"></image>
          <!-- {{item.wupinImg}} -->
          <view class="center_show"><text>描述:</text>{{item.wupinMiaoshu}}</view>
        </view>
        <view class="item_bottom">
          <view>{{item.wupinTime}}</view>
          <view><text>¥ {{item.wupinPic}}</text> <text>x {{item.wupinNum}}</text></view>
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
        list: "",
        user_id: "",
        swiperList: [
          {
            image: "http://m.qpic.cn/psc?/V14crKpG3H0KQu/45NBuzDIW489QBoVep5mcX1w9Fr68F9o.*hzEksAAWd1qYUQi7mBPCEjLig615IFWCbz4oSXy62udv*d*xcbZFnY5P.u0rclIlyfliwavis!/b&bo=YgPOAWIDzgEBGT4!&rf=viewer_4"
          },
          {
            image: "http://m.qpic.cn/psc?/V14crKpG3H0KQu/45NBuzDIW489QBoVep5mcX1w9Fr68F9o.*hzEksAAWcnEc5b5yJXqOTvx3D158IZ7BoQl7fWWEZlMp*A8nH6uk0ewXLoX*ygUZ2miAnbXa8!/b&bo=6AMyAugDMgIBGT4!&rf=viewer_4"
          },
          {
            image: "http://m.qpic.cn/psc?/V14crKpG3H0KQu/45NBuzDIW489QBoVep5mcX1w9Fr68F9o.*hzEksAAWdDlraGz.al.0tAImKueI149FHCYzxEH.f0RvE2Gs4IsH0.vhLInQ7XlPqR2CrNv6E!/b&bo=PwPWAT8D1gEBGT4!&rf=viewer_4"
          }
        ]
      }
    },
    onShow() {
    this.getList();
    },
    methods: {
      getList() {
        const users = uni.getStorageSync("userInfo");
        console.log("用户信息:")
        console.log(users);
        this.user_id = users.id;
        wx.request({
          url: domain + "/list",
          method: "POST" ,
          data: {
            userId: this.user_id,
          },
          success:(res) => {
            console.log(res)
            this.list = res.data.data;
            console.log(this.list)
          }
        })
      },
      // 跳转到新增物品页
      getAddwupin() {
        uni.navigateTo({
          url: "/pagesA/addwupin/addwupin"
        })
      },
      // 跳转到物品详情页
      getWupin() {
        uni.navigateTo({
          url: "/pagesB/wupin_detail/wupin_detail"
        })
      }
    }
  }
</script>

<style lang="scss">
  .index_head {
    display: flex;
    flex-direction: row;
    align-items: center;
    image {
      width: 50rpx;
      height: 50rpx;
      margin-left: 23rpx;
    }
    view {
      margin-left: 10rpx;
      font-size: 28rpx;
      font-family: PingFang SC;
      color: #282828;
    }
  }
  .swiper {
    margin-top: 10rpx;
  }
  .addShouna {
    width: 682rpx;
    height: 84rpx;
    background: #F5F5F5;
    border-radius: 12rpx;
    display: flex;
    align-items: center;
    justify-content: center;
    // position: fixed;
    // top: 450rpx;
    // left: 50%;
    // margin-left: -341rpx;
    margin: 50rpx auto;
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
