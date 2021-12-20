<template>
  <view>
    <view class="wupin">
      <view class="remark-box">
        <view class="title">新增描述:</view>
        <view class="title_rt">{{ remark.length }}/ 100 字</view>
      </view>
      <!-- <view class="txt">{{ remark }}</view> -->
      <view class="txt">
        <u-input 
          v-model="remark" 
          type="textarea" 
          :trim="true" 
          :maxlength="100" 
          :border="true" 
          :height="30"
          :auto-height="true" />
      </view>
      <view class="wupin_bottom">
        <image :src="src" mode="" @click="getTu()"></image>
        <view class="bottom_rt">
          <view class="rt">价格¥<input type="text" :value="pic" /></view>
          <view class="rt">数量x<input type="text" :value="number" style="margin-left: 8rpx;" /></view>
        </view>
      </view>
      <view style="background-color: #969696;height: 2rpx; width: 668rpx; margin-left: 20rpx;margin-top: 20rpx;"></view>
      <view class="wupin_tips">
          <view class="tips_top">
            <view>便签</view>
            <image src="../../static/iconfont/arrow-right.png" mode="" @click="getTips"></image>
          </view>
          <view style="background-color: #d19a66; height: 2rpx; width: 344rpx; margin-left: 344rpx;"></view>
          <view class="tips_bottom">
            <view></view>
            <view class="tipsBtm_rt">
              <u-tag
                :text="tipsName" 
                type="warning" 
                mode="dark"/>
            </view>
          </view>
      </view>
    </view>
    <u-popup
      v-model="tipsShow" 
      mode="bottom" 
      border-radius="14" 
      height="40%" 
      safe-area-inset-bottom=true
      closeable=true>
      <view class="tips_type">
        <u-tag 
          class="tips_name"
          v-for="(item,index) in tipsList" 
          :key="index" 
          :text="item.tipsName" 
          type="warning" 
          mode="light"
          @click="setTips(item.tipsName)" />
      </view>
    </u-popup>
    
    <!-- 选择物品存放的盒子 -->
    <view class="wupin_box" @click="getBox">
      <text>选择存放盒子</text>
      <view style="display: flex; align-items: center;">
        <text>{{wupinTips}}</text>
        <image src="../../static/iconfont/arrow-right.png" mode=""></image>
      </view>
    </view>
    <u-popup v-model="wupinBox" mode="bottom" border-radius="14" height="60%" safe-area-inset-bottom="true"
      closeable="true">
      <text style=" position: fixed; top: 28rpx; left: 50%; margin-left: -101rpx;">选择物品存放的盒子</text>
      <view style="width: 100%; height: 83rpx; background-color: #FFFFFF;"></view>
      <scroll-view scroll-y="true" style="height: 450rpx;">
        <u-radio-group v-model="radio" active-color="#d19a66" wrap="true" width="100%" @change="setRadio">
          <u-radio name="0">
            <view class="box_item">
              <view class="item_head">
                <text>BX0001</text>
                <image src="../../static/iconfont/xiugai@2x.png" mode="" @click="getBoxdetail"></image>
              </view>
              <view class="item_center">
                <text>盒子名称</text>
                <text>盒子类型</text>
              </view>
            </view>
          </u-radio>
          <u-radio name="1">
            <view class="box_item">
              <view class="item_head">
                <text>BX0002</text>
                <image src="../../static/iconfont/xiugai@2x.png" mode="" @click="getBoxdetail"></image>
              </view>
              <view class="item_center">
                <text>盒子名称</text>
                <text>盒子类型</text>
              </view>
            </view>
          </u-radio>
        </u-radio-group>
      </scroll-view>
      <view class="addBox">
        <image src="../../static/iconfont/add_shouna.png" mode=""></image>
        <text>新增收纳盒子</text>
      </view>
    </u-popup>
    <!-- 选择物品过期的时间 -->
    <view class="wupin_box" @click="getTime">
      <text>选择过期时间</text>
      <view style="display: flex; align-items: center;">
        <text>{{time}}</text>
        <image src="../../static/iconfont/arrow-right.png" mode=""></image>
      </view>
    </view>
    <u-calendar 
      v-model="timeBox" 
      :mode="mode" 
      @change="change" 
      :safe-area-inset-bottom="false" 
      maxDate="2100-01-01"
      toolTip="选择过期时间" 
      btn-type=warning 
      active-bg-color=#e17f4b>
    </u-calendar>
    <!-- 底部保存按钮 -->
    <button type="default" class="buttom">修改保存</button>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        keyword: "",
        remark: "",
        pic: "",
        number: "",
        src: "../../static/img/pic_add.png",
        wupinTips: "",
        timeBox: false,
        wupinBox: false,
        mode: 'date',
        time: "",
        radio: "0",
        tipsName: "选择类型",
        tipsShow: false,
        tipsList: [
          {tipsName: "衣服"},
          {tipsName: "裤子"},
          {tipsName: "鞋子"},
          {tipsName: "帽子"},
          {tipsName: "包包"},
          {tipsName: "美妆"},
          {tipsName: "数码"},
          {tipsName: "食物"},
          {tipsName: "书籍"},
          {tipsName: "首饰"},
          {tipsName: "袜子"},
          {tipsName: "工具"},
          {tipsName: "厨具"},
          {tipsName: "用品"},
          {tipsName: "文具"},
          {tipsName: "体育"},
          {tipsName: "车类"},
          {tipsName: "乐器"},
          {tipsName: "酒类"},
          {tipsName: "电器"},
          {tipsName: "贵重"},
          {tipsName: "其他"}
        ]
      }
    },
    methods: {
      // 选择物品图片
      getTu() {
        uni.chooseImage({
          count: 1,
          success: (res) => {
            this.src = res.tempFilePaths;
            console.log(JSON.stringify(res.tempFilePaths));
          }
        })
      },
      // 选择盒子
      getBox() {
        this.wupinBox = true
      },
      setRadio() {
        this.wupinBox = false
        this.wupinTips = "BX0001"
      },
      // 选择过期时间
      getTime() {
        this.timeBox = true
      },
      change(e) {
        console.log(e)
        this.time = e.result
      },
      // 选择物品类别
      getTips() {
        this.tipsShow = true
      },
      setTips(tips) {
        console.log(tips)
        this.tipsName = tips
        this.tipsShow = false
      },
      // 跳转到盒子详情页
      getBoxdetail() {
        uni.navigateTo({
          url: "../../pagesB/box_detail/box_detail"
        })
      }
    }
  }
</script>

<style lang="scss">
  .wupin {
    width: 688rpx;
    min-height: 300rpx;
    background: #ffffff;
    box-shadow: 0rpx 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.05);
    border-radius: 8rpx;
    margin: 27rpx auto 0;
    color: #333333;
    font-size: 32rpx;
    padding-bottom: 20rpx;
    padding-top: 20rpx;

    .remark-box {
      margin: 0rpx 26rpx 0;
      display: flex;
      justify-content: space-between;

      .title {
        font-size: 32rpx;
        font-family: PingFang SC;
        font-weight: 500;
        color: #333333;
      }

      .title_rt {
        font-size: 32rpx;
        font-family: PingFang SC;
        font-weight: 500;
        color: #CECECE;
      }
    }
    .txt {
      width: 642rpx;
      border: -1rpx solid #EBEBEB;
      color: #cecece;
      font-size: 24rpx;
      margin: 20rpx auto;
      margin-bottom: 10rpx;
    }

    .wupin_bottom {
      display: flex;
      justify-content: space-between;

      .bottom_rt {
        font-size: 30rpx;
        display: flex;
        flex-direction: column;

        .rt {
          display: flex;
          flex-direction: row;
          margin-top: 22rpx;
          margin-right: 24rpx;
          color: #de3121;

          input {
            border: 2rpx solid #dedede;
            width: 70rpx;
            color: #222222;
            margin-left: 5rpx;
          }
        }
      }

      image {
        width: 130rpx;
        height: 130rpx;
        margin-left: 24rpx;
        margin-top: 15rpx;
      }
    }
    .wupin_tips {
      .tips_top {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 20rpx 20rpx 0 20rpx;
        image {
          width: 50rpx;
          height: 50rpx;
        }
      }
      .tips_bottom {
        display: flex;
        justify-content: space-between;
        margin-right: 20rpx;
        margin-top: 10rpx;
      }
    }
  }
  .tips_type {
    margin-top: 80rpx;
    padding: 0 20rpx;
    display: flex;
    flex-wrap: wrap;
    margin-left: 20rpx;
    .tips_name {
      margin: 10rpx; 
    }
  }
  .wupin_box {
    width: 688rpx;
    height: 80rpx;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 32rpx;
    box-shadow: 0px 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.1);
    margin: 20rpx auto;

    text {
      margin-left: 20rpx;
    }

    image {
      width: 50rpx;
      height: 50rpx;
      margin-right: 20rpx;
    }
  }

  .box_item {
    width: 688rpx;
    margin-top: 20rpx;
    box-shadow: 0px 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.1);
    padding: 20rpx;
    border-bottom: 2rpx solid #a1a1a1;
    .item_head {
      display: flex;
      justify-content: space-between;
      font-size: 32rpx;
      font-family: PingFang SC;
      font-weight: bold;
      color: #2C2C2C;
      image {
        width: 46rpx;
        height: 46rpx;
      }
    }
    .item_center {
      display: flex;
      justify-content: space-between;
      margin-top: 20rpx;
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
  .buttom {
    width: 640rpx;
    height: 84rpx;
    position: fixed;
    bottom: 20rpx;
    left: 50%;
    margin-left: -320rpx;
    background-color: #e19d3e !important;
  }
</style>
