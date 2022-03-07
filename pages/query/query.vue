<template>
  <view>
    <view class="search">
      <view class="search-lf" @click="getSearch()">
        <image src="../../static/iconfont/search_icon.png" mode=""></image>
        <text>输入关键字进行检索</text>
      </view>
      <view @click="saoma">
        <image src="../../static/iconfont/search.png" mode=""></image>
      </view>
    </view>

    <view class="search_center">

      <view class="shouna_item" v-for="(item,index) in list" :key="item.index" @click="getWupin(index)">
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
        list: "", //请求到的数据数组
        user_id: "", //用户id
      }
    },
    onShow() {
      this.getList();
    },
    methods: {
      // 请求数据
      getList() {
        const users = uni.getStorageSync("userInfo");
        // console.log("用户信息:")
        // console.log(users);
        this.user_id = users.id;
        console.log(this.user_id + "参数")
        wx.request({
          url: domain + "/list",
          method: "POST",
          data: {
            userId: this.user_id,
          },
          success: (res) => {
            console.log(res)
            this.list = res.data.data;
            console.log(this.list)
          }
        })
      },
      // 跳转到搜索页面
      getSearch() {
        uni.navigateTo({
          url: "../../pagesA/search/search"
        })
      },
      // 二维码扫描
      saoma() {
        uni.scanCode({
          success: function(res) {
            console.log('条码类型：' + res.scanType);
            // console.log('条码内容：' + res.result);
            let result = res.result
            console.log("1" + result)
            // 跳转到二维码详情页
            uni.navigateTo({
              url: "../../pagesB/QRcode/QRcode?txt=" + encodeURIComponent(JSON.stringify(result))
            })
          }
        });
      },
      // 跳转到物品详情页
      getWupin(index) {
        let boxId = this.list[index].id;
        uni.navigateTo({
          url: "/pagesB/wupin_detail/wupin_detail?boxId=" + boxId
        })
      }
    }
  }
</script>

<style lang="scss">
  page {
    background-color: #f5f5f5;
  }
  .search {
    width: 688rpx;
    height: 80rpx;
    margin: 20rpx auto;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;

    .search-lf {
      border: 1rpx solid #a1a1a1;
      border-radius: 40rpx;
      width: 400rpx;
      display: flex;
      align-items: center;
      font-size: 22rpx;
      color: #a1a1a1;

      image {
        width: 60rpx;
        height: 60rpx;
        margin-left: 20rpx;
      }

      text {
        margin-left: 10rpx;
      }
    }

    image {
      width: 70rpx;
      height: 70rpx;
    }
  }

  .search_center {
    .shouna_item {
      margin: 30rpx auto 0;
      padding-bottom: 20rpx;
      width: 688rpx;
      min-height: 328rpx;
      box-shadow: 0px 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.1);
      border-radius: 8rpx;
      background-color: #FFFFFF;

      .item_head {
        display: flex;
        justify-content: space-between;

        .head_lf {
          display: flex;
          align-items: center;

          image {
            width: 50rpx;
            height: 50rpx;
            margin-top: -10rpx;
          }
        }

        .head_rt {
          margin: 15rpx 30rpx 0 0;
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
        padding: 0 30rpx;
        margin-top: 20rpx;

        text {
          margin-right: 10rpx;
        }
      }
    }
  }
</style>
