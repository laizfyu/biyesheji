<template>
  <view>
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
            <u-input v-model="name" type=text focus maxlength=10 />
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
        <view class="img">
          <image :src="boxImg" mode=""></image>
          <view class="changeImg" @click="getImg">更改盒子照片</view>
        </view>
      </view>
      <!-- 盒子二维码 -->
      <view class="box_img">
        <view class="title">盒子二维码</view>
        <view class="img">
          <image :src="erWei" mode=""></image>
        </view>
      </view>
    </view>
    <!-- 提示 -->
    <u-toast ref="uToast" />
    <!-- 底部保存按钮 -->
    <button type="default" class="buttom" @click="changeBox">确认修改</button>
    <view class="close_box" @click="closeBox">删除盒子</view>
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
        // value: "", //更改的盒子名字
        input: "", //盒子描述
        boxImg: "/static/img/pic_add.png", //盒子照片
        erWei: "", //盒子二维码
        closeable: false,
        detail: "", //上个页面数据
        id: "", //盒子对应的id
      }
    },
    onLoad(options) {
      this.detail = JSON.parse(decodeURIComponent(options.detail));
      console.log(this.detail);
      this.name = this.detail.boxName;
      this.input = this.detail.boxMiaoshu;
      this.id = this.detail.id;
      console.log(this.id + ":id"); 
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
        if (this.name.length == 0) {
          console.log("不能为空",this.name)
          this.$refs.uToast.show({
            title: '盒子名字不能为空',
            type: 'warning',
          })
        } 
      },
      // 选择盒子照片
      getImg() {
        uni.chooseImage({
          count: 1,
          success: (res) => {
            this.boxImg = res.tempFilePaths[0];
            console.log(this.boxImg);
          },
          fail: (err)=> {
            console.log(err)
            this.$refs.uToast.show({
              title: '获取图片失败',
              type: 'error',
            })
          }
        })
      },
      changeBox() {
        wx.request({
          url: domain + "/editBox",
          method: "PUT",
          data: {
            boxName: this.name,
            boxImg: this.boxImg,
            boxMiaoshu: this.input,
            id: this.id
          },
          success: (save) => {
            console.log(save)
            this.$refs.uToast.show({
              title: save.data.msg,
              type: 'success',
            })
            setTimeout(() => {
              uni.reLaunch({
                url: "/pagesA/box/box"
              })
            }, 1000);
          }
        })
      },
      closeBox() {
        
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
    .changeImg {
      width: 200rpx;
      height: 50rpx;
      text-align: center;
      line-height: 50rpx;
      color: #FFFFFF;
      font-size: 28rpx;
      margin: 10rpx auto;
      background-color: #e19d3e;
    }
  }

  .buttom {
    width: 640rpx;
    height: 84rpx;
    margin: 100rpx auto;
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
  .close_box {
    font-size: 28rpx;
    color: red;
    width: 200rpx;
    height: 50rpx;
    text-align: center;
    line-height: 50rpx;
    margin: 0rpx auto;
  }
</style>
