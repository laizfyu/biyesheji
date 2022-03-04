<template>
  <view class="box">
    <!-- 输入盒子的名称 -->
    <view class="box_name">
      <view class="name_head">
        <view>盒子名称</view>
        <view @click="getShow" style="min-width: 50rpx; min-height: 30rpx; color: #d49a67;">{{name}}</view>
      </view>
      <view class="name_bottom">
        <view>盒子标签</view>
        <view style="color: #d49a67;">{{detail.boxId}}</view>
        <!-- <image src="../../static/iconfont/arrow-right.png" mode=""></image> -->
      </view>
      <!-- <view class="name_bottom">
        <view>盒子类型</view>
        <view style="color: #d49a67;" @click="getType()">{{typeName}}</view>
        <!-- <image src="../../static/iconfont/arrow-right.png" mode=""></image> -->
      <!-- </view> -->
    </view>
    <u-modal 
      show-cancel-button 
      v-model="show" 
      title="请输入盒子名称" 
      @confirm="setModal" 
      confirm-color="#dea36c">
      <view class="slot-content">
        <view class="ipt">
          <u-input v-model="value" type=text focus maxlength=10 />
        </view>
      </view>
    </u-modal>
    <!-- 位置信息详细描述 -->
    <view class="info">
      <view class="info_head">
        <text>信息描述:</text>
        <text>{{ input.length }}/ 100字</text>
      </view>
      <u-input 
        type="textarea" 
        v-model="input" 
        placeholder="请输入盒子描述(收纳物品详情或盒子位置)" 
        height="120" 
        border=true
        borderColor="#dea36c" 
        maxlength="100" 
        focus=false>
      </u-input>
    </view>
    <!-- 选择照片 -->
    <view class="box_img">
      <view class="title">盒子照片</view>
      <view class="img" @click="getImg">
        <image :src="boxImg" mode=""></image>
      </view>
    </view>
    <!-- 盒子二维码 -->
    <view class="box_img">
      <view class="title">盒子二维码</view>
      <view class="img">
        <image :src="erWei" mode=""></image>
      </view>
    </view>
    <!-- 底部保存按钮 -->
    <button type="default" class="buttom">确认修改</button>
    <!-- 提示 -->
    <u-toast ref="uToast" />
    <!-- 盒子类型选择 -->
    <!-- <u-popup
      v-model="typeShow" 
      mode="bottom" 
      border-radius="14" 
      height="30%" 
      safe-area-inset-bottom=true
      closeable=true>
      <view class="box_type">
        <u-tag 
          class="type_name"
          v-for="(item,index) in list" 
          :key="index" 
          :text="item.typeName" 
          type="warning" 
          mode="light"
          @click="setType(item.typeName)"
          :closeable="closeable" />
      </view>
    </u-popup> -->
  </view>
</template>

<script>
  const app = getApp()
  const domain = app.globalData.domain
  export default {
    data() {
      return {
        name: "", //盒子名字
        show: false, //名字更改显示
        // typeShow: false,
        value: "", //更改的盒子名字
        input: "", //盒子描述
        boxImg: "http://tmp/QB5i6HNddimMd87e0c0e97e16b9639e2701a8b36439c.jpg", //盒子照片
        erWei: "", //盒子二维码
        closeable: false,
        detail: ""
      }
    },
    onLoad(options) {
      this.detail = JSON.parse(decodeURIComponent(options.detail));
      console.log(this.detail);
      this.name = this.detail.boxName;
      this.input = this.detail.boxMiaoshu;
      if(this.detail.boxImg) {
        this.boxImg = this.detail.boxImg;
      }
      this.erWei = this.detail.boxErwei;
    },
    methods: {
      // 填写盒子名称
      getShow() {
        this.show = true
      },
      setModal() {
        if (this.value.length == 0) {
          console.log("不能为空",this.name)
          this.$refs.uToast.show({
            title: '盒子名字不能为空',
            type: 'warning',
          })
        } else {
          this.name = this.value
        }
      },
      // 选择盒子照片
      getImg() {
        uni.chooseImage({
          count: 1,
          success: (res) => {
            this.boxImg = res.tempFilePaths;
            console.log(this.boxImg);
            // wx.request({
            //   url: domain + "/avatar",
            //   method: "POST",
            //   data: {
                
            //   }
            // })
          },
          fail: ()=> {
            console.log("出错啦")
            this.$refs.uToast.show({
              title: '获取图片失败',
              type: 'error',
            })
          }
        })
      }
    }
  }
</script>

<style lang="scss">
  .box {
    width: 720rpx;
    min-height: 1140rpx;
    background: #fcfcfc;
    box-shadow: 0rpx 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.1);
    margin: 10rpx auto;
    padding-top: 10rpx;
    padding-bottom: 100rpx;
  }

  .box_name {
    // height: 90rpx;
    // line-height: 80rpx;
    border-bottom: 2rpx solid #dea36c;
    padding: 30rpx;

    .name_head {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .name_bottom {
      margin-top: 20rpx;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
  }

  .info {
    width: 688rpx;
    min-height: 200rpx;
    background: #ffffff;
    box-shadow: 0rpx 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.05);
    border-radius: 8rpx;
    margin: 27rpx auto 0;
    color: #333333;
    font-size: 32rpx;
    padding: 20rpx;

    .info_head {
      display: flex;
      justify-content: space-between;
      margin-bottom: 20rpx;
    }
  }

  .box_img {
    margin-top: 50rpx;
    width: 100%;

    .title {
      margin-left: 20rpx;
      font-size: 30rpx;
      font-weight: 500;
    }

    .img {
      width: 500rpx;
      height: 500rpx;
      margin: 20rpx auto;

      image {
        width: 100%;
        height: 100%;
      }
    }
  }

  .buttom {
    width: 640rpx;
    height: 84rpx;
    position: fixed;
    bottom: 20rpx;
    left: 50%;
    margin-left: -320rpx;
    background-color: #e19d3e !important;
  }
 .box_type {
    margin-top: 80rpx;
    padding: 0 20rpx;
    display: flex;
    flex-wrap: wrap;
    .type_name {
      margin: 20rpx;
      
    }
  }
  .ipt {
    padding: 10rpx 20rpx;
  }
</style>
