<template>
  <view>
    <!-- 物品详情 -->
    <view class="wupin_name">
      <view>名称:</view>
      <view>短袖</view>
    </view>
    <view class="line"></view>
    <view class="wupin_name">
      <view>标签:</view>
      <view>fx0001</view>
    </view>
    <view class="line"></view>
    <view class="wupin_name">
      <view>价格数量:</view>
      <view><text>¥ 5</text> <text>x 2</text></view>
    </view>
    <view class="line"></view>
    <view class="wupin_name">
      <view>物品类别:</view>
      <view>衣服</view>
    </view>
    <view class="line"></view>
    <view class="wupin_name">
      <view>物品所在家庭:</view>
      <view>vqerb</view>
    </view>
    <view class="line"></view>
    <!-- <view class="detail_head">
      <view class="head_top">
        <view class="bkg"><text>XF0001</text></view>
        <view>名字</view>
      </view>
      <view class="head_center">
        <image :src="wupinImg" mode="aspectFit" @click="getWupinimg"></image>
        <u-input 
          style="width: 500rpx;"
          v-model="WPdetail" 
          type="textarea" 
          border="true" 
          autoHeight="true" 
          height="135" 
          borderColor="#d69d68"/>
      </view>
      <view class="head_btm">
        <view>2021/01/01</view>
        <view>
          <u-tag
            :text="wupintips" 
            type="warning" 
            mode="dark"/>
        </view>
      </view>
      <view class="head_btm">
        <view></view>
        <view style="color: #d69d68; font-size: 22rpx;"><text>¥ 5</text> <text>x 2</text></view>
      </view>
    </view> -->
    <!-- 物品二维码 -->
    <!-- <view class="wupin_QRcode">
      <view style="margin-left: 20rpx;">物品二维码:</view>
      <view class="QRcode" @click="getWupinimg"><image :src="wupinQRcode" mode=""></image></view>
    </view> -->
    <!-- 物品所存盒子 -->
    <view style="margin: 20rpx;">物品所存盒子:</view>
    <view class="wupinBox">
      <view class="wupinBox_head">
        <view class="bkg"><text>小明的鞋架</text></view>
        <!-- <image src="../../static/iconfont/arrow-right.png" mode="" @click="getBoxdetail"></image> -->
      </view>
      <view class="wupinBox_center">
        <image :src="boxImg" mode="aspectFit" @click="getWupinimg"></image>
        <u-input 
        style="width: 500rpx;" 
        v-model="BXdetail" 
        type="textarea" 
        border="none" 
        autoHeight="true"
        disabled="true" 
        height="135" />
      </view>
    </view>
    <view class="line"></view>
    <!-- 物品照片 -->
    <view style="margin: 20rpx;">物品照片:</view>
    <view class="wupin_img">
      <image src="/static/img/jiaju.webp" mode="aspectFit"></image>
    </view>
    <!-- 底部按钮 -->
    <button type="default" class="buttom" @click="getWupinChange">物品变更</button>
  </view>
</template>

<script>
  const app = getApp()
  const domain = app.globalData.domain
  export default {
    data() {
      return {
        WPdetail: "", //物品详细描述
        BXdetail: "夏天穿的短袖,放在衣柜角落", //盒子详细描述
        wupintips: "鞋子", //物品类型标签
        boxtips: "鞋柜", //盒子类型标签
        wupinImg: "../../static/img/touxiang.jpg", //物品图片
        wupinQRcode: "../../static/img/erwei_test.jpg", //物品二维码
        boxImg: "../../static/img/jiaju.webp", //盒子图片
        ID: ""
      }
    },
    onLoad(options) {
      this.ID = options.boxId;
      console.log(this.ID);
      this.getDetail();
    },
    methods: {
      // 请求物品详情数据
      getDetail() {
        wx.request({
          url: domain + "/getWuPin?id=" + this.ID,
          method: "GET",
          success: (res) => {
            console.log(res)
          }
        })
      },
      // 跳转到盒子详情页
      // getBoxdetail() {
      //   uni.navigateTo({
      //     url: "../box_detail/box_detail"
      //   })
      // },
      getWupinimg() {
        let listImg = [this.wupinImg, this.wupinQRcode, this.boxImg];
        console.log("listImg:" + listImg);
        uni.previewImage({
          current: 0,
          urls: listImg,
          // longPressActions: {
          //   itemList: ['保存图片', '更改图片','取消'],
          //   success:(data) => {
          //     console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data.index + 1) + '张图片');
          //     console.log(this.listImg)
          //   },
          //   fail(res) {
          //     console.log(res)
          //   }
          // }
          // success: (res) => {
          //   console.log(res)
          // },
          // fail: (err) => {
          //   console.log(err)
          // }
        })
      },
      getWupinChange() {
        uni.navigateTo({
          url: "../wupin_change/wupin_change"
        })
      }
    }
  }
</script>

<style lang="scss">
  .wupin_name {
    min-height: 68rpx;
    display: flex;
    justify-content: space-between;
    line-height: 68rpx;
    font-size: 26rpx;
    font-family: PingFang SC;
    font-weight: 500;
    color: #666666;
    padding: 0 20rpx;
  }

  .line {
    height: 12rpx;
    background: #F2F2F2;
  }

  .bkg {
    min-width: 120rpx;
    height: 50rpx;
    line-height: 50rpx;

    text {
      margin-left: 10rpx;
    }
  }

  .wupin_QRcode {
    margin-top: 30rpx;

    .QRcode {
      margin: 20rpx auto;
      width: 500rpx;
      height: 500rpx;

      image {
        width: 100%;
        height: 100%;
      }
    }
  }

  .wupinBox {
    width: 688rpx;
    min-height: 200rpx;
    background: #ffffff;
    box-shadow: 0rpx 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.05);
    margin: 20rpx auto;
    padding: 20rpx;
    font-size: 26rpx;
    font-family: PingFang SC;
    font-weight: 500;
    color: #666666;

    .wupinBox_head {
      display: flex;
      justify-content: space-between;
      align-items: center;

      image {
        width: 36rpx;
        height: 36rpx;
      }
    }

    .wupinBox_center {
      display: flex;
      flex-direction: row;
      align-items: center;
      margin-top: 20rpx;

      image {
        width: 150rpx;
        height: 150rpx;
        margin-right: 10rpx;
      }
    }

    .wupinBox_btm {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 20rpx;
    }
  }

  .wupin_img {
    width: 400rpx;
    height: 400rpx;
    margin: 10rpx auto;
    
    image {
      width: 100%;
      height: 100%;
    }
  }
  
  .wupinFamily {
    width: 688rpx;
    min-height: 200rpx;
    background: #ffffff;
    box-shadow: 0rpx 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.05);
    margin: 20rpx auto;
    padding: 20rpx;

    .wupinFamily_hd {
      display: flex;
      justify-content: space-between;
      align-items: center;

      image {
        width: 36rpx;
        height: 36rpx;
      }
    }

    .wupinFamily_ct {
      display: flex;
      flex-direction: row;
      margin-top: 10rpx;

      image {
        width: 200rpx;
        height: 200rpx;
      }

      .wpFyct_rt {
        margin-left: 20rpx;
        color: #d19a66;

        image {
          width: 50rpx;
          height: 50rpx;
          margin-right: 10rpx;
        }

        .family_member {
          display: flex;
          align-items: center;
          margin-bottom: 50rpx;
          margin-top: 20rpx;
        }
      }
    }
  }

  .buttom {
    width: 640rpx;
    height: 84rpx;
    margin-top: 100rpx;
    margin-bottom: 50rpx;
    left: 50%;
    margin-left: -320rpx;
    background-color: #e19d3e !important;
  }
</style>
