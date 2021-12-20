<template>
  <view>
    <!-- 物品详情 -->
    <view class="detail_head">
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
    </view>
    <!-- 物品二维码 -->
    <view class="wupin_QRcode">
      <view style="margin-left: 20rpx;">物品二维码:</view>
      <view class="QRcode"><image :src="wupinQRcode" mode=""></image></view>
    </view>
    <!-- 物品所存盒子 -->
    <view style="margin: 20rpx;">物品所存盒子:</view>
    <view class="wupinBox">
      <view class="wupinBox_head">
        <view class="bkg"><text>Bx0001</text></view>
        <image src="../../static/iconfont/arrow-right.png" mode="" @click="getBoxdetail"></image>
      </view>
      <view class="wupinBox_center">
        <image :src="boxImg" mode="aspectFit"></image>
        <u-input 
          style="width: 500rpx;"
          v-model="BXdetail" 
          type="textarea" 
          border="true" 
          autoHeight="true" 
          height="135" 
          borderColor="#d69d68"/>
      </view>
      <view class="wupinBox_btm">
        <view>小明的鞋架</view>
        <view>
          <u-tag
            :text="boxtips" 
            type="warning" 
            mode="dark"/>
        </view>
      </view>
    </view>
    <!-- 底部按钮 -->
    <button type="default" class="buttom" @click="getWupinChange">物品记录变更</button>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        WPdetail: "", //物品详细描述
        BXdetail: "", //盒子详细描述
        wupintips: "鞋子", //物品类型标签
        boxtips: "鞋柜", //盒子类型标签
        wupinImg: "../../static/img/touxiang.jpg", //物品图片
        wupinQRcode: "../../static/img/pic_add.png", //物品二维码
        boxImg: "../../static/img/jiaju.webp", //盒子图片
        listImg: [
          "../../static/img/touxiang.jpg",
          "../../static/img/pic_add.png",
          "../../static/img/jiaju.webp"
          ]
      }
    },
    methods: {
      // 跳转到盒子详情页
      getBoxdetail() {
        uni.navigateTo({
          url: "../box_detail/box_detail"
        })
      },
      getWupinimg() {
        uni.previewImage({
          urls: this.listImg,
          longPressActions: {
            itemList: ['保存图片', '更改图片','取消'],
            success:(data) => {
              console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data.index + 1) + '张图片');
              console.log(this.listImg)
            },
            fail(res) {
              console.log(res)
            }
          }
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
  .detail_head {
    width: 688rpx;
    min-height: 200rpx;
    background: #ffffff;
    box-shadow: 0rpx 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.05);
    margin: 20rpx auto;
    padding: 20rpx;
    .head_top {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .head_center {
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
    .head_btm {
      display: flex;
      justify-content: space-between;
      margin-top: 20rpx;
      text {
        margin-left: 10rpx;
      }
    }
  }
  .bkg {
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
  .wupin_QRcode {
    margin-top: 30rpx;
    // margin-left: 20rpx;
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
