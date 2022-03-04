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

      <view class="shouna_item" @click="getWupinDetail">
        <view class="item_head">
          <view class="head_lf">
            <image src="../../static/iconfont/add_item.png" mode=""></image>
            <text>XF0001</text>
          </view>
          <text class="head_rt">饮料</text>
        </view>
        <view class="item_center">
          <image src="../../static/img/pic_add.png" mode="aspectFit"></image>
          <view class="center_show">
            <text>描述:</text>编译成功。前端运行日志，请另行在小程序开发工具的控制台查看。编译成功。前端运行日志，请另行在小程序开发工具的控制台查看编译成功。前端运行日志，请另行在小程序开发工具的控制台查看
          </view>
        </view>
        <view class="item_bottom">
          <view>2021/12/09</view>
          <view><text>¥ {{pic}}</text> <text>x {{number}}</text></view>
        </view>
      </view>

    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        pic: 5,
        number: 2
      }
    },
    methods: {
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
            console.log("1"+result)
            // 跳转到二维码详情页
            uni.navigateTo({
              url: "../../pagesB/QRcode/QRcode?txt=" + encodeURIComponent(JSON.stringify(result))
            })
          }
        });
      },
      // 跳转到物品详情页
      getWupinDetail() {
        uni.navigateTo({
          url: "../../pagesB/wupin_detail/wupin_detail"
        })
      }
    }
  }
</script>

<style lang="scss">
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
