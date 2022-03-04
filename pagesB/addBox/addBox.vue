<template>
  <view class="box">
    <!-- 输入盒子的名称 -->
    <view class="box_name">
      <text>盒子名称</text>
      <view class="name" @click="getShow">
        <text>{{name}}</text>
        <image src="../../static/iconfont/arrow-right.png" mode=""></image>
      </view>
    </view>
    <u-modal 
      show-cancel-button 
      v-model="show" 
      title="请输入盒子名称" 
      @confirm="setModal" 
      confirm-color="#dea36c">
      <view class="slot-content">
        <view class="ipt">
          <u-input v-model="value" type=text focus maxlength=6 />
        </view>
      </view>
    </u-modal>

    <!-- 盒子类型 -->
   <!-- <view class="box_name">
      <text>盒子类型</text>
      <view class="name" @click="getType">
        <text>{{typeName}}</text>
        <image src="../../static/iconfont/arrow-right.png" mode=""></image>
      </view>
    </view>
    <u-popup 
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
    </u-popup>
 -->
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
        maxlength="100">
        </u-input>
    </view>
    <!-- 选择照片 -->
    <view class="box_img">
      <view class="title">选择照片</view>
      <view class="img" @click="getImg">
        <image :src="boxImg" mode=""></image>
      </view>
    </view>
    <!-- 提示 -->
    <u-toast ref="uToast" />
    <view class="news">
      盒子标签以及二维码将会自动生成
    </view>
    <!-- 底部保存按钮 -->
    <button type="default" class="buttom" @click="saveBox">保存</button>
  </view>
</template>

<script>
  const app = getApp()
  const domain = app.globalData.domain
  export default {
    data() {
      return {
        name: "", //盒子名称
        show: false,
        typeShow: false,
        value: "",
        input: "", //盒子描述
        boxImg: "/static/img/pic_add.png", //盒子图片
        typeName: "",
        closeable: false,
        user_id: "", //用户id
        user_name: "", //用户姓名
      }
    },
    methods: {
      // 填写盒子名称
      getShow() {
        this.show = true
        const users = uni.getStorageSync("userInfo");
        this.user_id = users.userId;
        this.user_name = users.userName;
      },
      setModal() {
        if (this.value.length == 0) {
          console.log("不能为空", this.name)
          this.$refs.uToast.show({
            title: '盒子名字不能为空',
            type: 'warning',
          })
        } else {
          this.name = this.value
        }
      },
      // 填写盒子类型
      getType() {
        this.typeShow = true
      },
      setType(res) {
        console.log(res)
        this.typeName = res
        this.typeShow = false
      },
      // 选择盒子照片
      getImg() {
        uni.chooseImage({
          count: 1,
          success: (res) => {
            this.boxImg = res.tempFilePaths[0]
            console.log(this.boxImg);
          },
          fail: () => {
            console.log("出错啦")
          }
        })
      },
      saveBox() {
        wx.request({
          url: domain + "/saveBox",
          method: "POST",
          data: {
            boxName: this.name,
            boxImg: this.boxImg,
            userId: this.user_id,
            userName: this.user_name,
            boxMiaoshu: this.input
          },
          success(res) {
            console.log(res)
            uni.navigateBack({
              
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
  }

  .box_name {
    height: 90rpx;
    line-height: 80rpx;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 2rpx solid #dea36c;
    padding: 30rpx;

    image {
      width: 36rpx;
      height: 36rpx;
    }

    .name {
      display: flex;
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

  .box_type {
    margin-top: 80rpx;
    padding: 0 20rpx;
    display: flex;
    flex-wrap: wrap;
    .type_name {
      margin: 20rpx;
      
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

  .news {
    font-size: 26rpx;
    color: #828282;
    position: absolute;
    // bottom: 10rpx;
    left: 50%;
    margin-left: -90px;
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

  .ipt {
    padding: 10rpx 20rpx;
  }
</style>
