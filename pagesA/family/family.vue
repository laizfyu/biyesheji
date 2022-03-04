<template>
  <view>
    <view class="familyItem" v-for="(item,index) in familyList" :key="item.index">
      <view class="news_head">
        <view class="head_lf">
          <image src="../../static/iconfont/family_item.png" mode=""></image> 
          <view class="bkg"><text>{{item.familyId}}</text></view>
        </view>
        <view class="head_rt" @click="getFamily(index)">
          <view>{{item.familyName}}</view>
          <image src="../../static/iconfont/arrow-right.png" mode=""></image>
        </view>
        
      </view>
      <!-- <view class="news_center">
        <image src="../../static/img/pic_add.png" mode="aspectFit"></image>
        <view class="familyNews">
          <image src="../../static/iconfont/item.png" mode=""></image>
          <!-- <view>成员: {{number}}</view> -->
        <!-- </view>
      </view> --> 
      <!-- <view class="news_bottom">
        <view></view>
        
      </view> -->
    </view>
    <button type="default" class="buttom" @click="addFamily">组建家庭</button>
    <u-modal
      show-cancel-button 
      v-model="show" 
      title="请输入家庭名称" 
      @confirm="setModal" 
      confirm-color="#dea36c">
      <view class="slot-content">
        <view class="ipt">
          <u-input v-model="value" type=text focus maxlength=10 />
        </view>
      </view>
    </u-modal>
  </view>
</template>

<script>
  const app = getApp()
  const domain = app.globalData.domain
  export default {
    data() {
      return {
        number: 8,
        userId: "",
        familyList: "",
        show: false,
        value: ""
      }
    },
    onShow() {
      const users = uni.getStorageSync("userInfo");
      this.userId = users.id;
      console.log(this.userId)
      this.getList() 
    },
    methods: {
      getList() {
        wx.request({
          url: domain + "/familyList?userId=" + this.userId,
          method: "GET",
          // data: {
          //   userId: this.userId
          // },
          success:(res) => {
            // console.log(res)
            this.familyList = res.data.data;
            console.log(this.familyList);
          }
        })
      },
      getFamily(index) {
        let detail = this.familyList[index];
        uni.navigateTo({
          url: "../../pagesB/family_detail/family_detail?detail=" + encodeURIComponent(JSON.stringify(detail)),
        })
      },
      
      // 新建家庭
      addFamily() {
        this.show = true;
        console.log(this.show)
      },
      setModal() {
        if (this.value.length == 0) {
          console.log("不能为空")
          this.$refs.uToast.show({
            title: '家庭名称不能为空',
            type: 'warning',
          })
        } else {
          wx.request({
            url: domain + "/addFamily",
            method: "POST",
            data: {
              familyName: this.value
            },
            success(addfm) {
              console.log(addfm);
            }
          })
        }
      },
    }
  }
</script>

<style lang="scss">
  .familyItem {
    width: 688rpx;
    min-height: 50rpx;
    background: #ffffff;
    box-shadow: 0rpx 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.05);
    border-radius: 8rpx;
    margin: 27rpx auto 0;
    padding: 20rpx;
    .news_head {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 30rpx;
      font-family: PingFang SC;
      font-weight: 500;
      color: #2C2C2C;
      .head_lf {
        display: flex;
        flex-direction: row;
        align-items: center;
        .bkg {
          // background-image: url(../../static/iconfont/tips@2x%20.png);
          // background-size: cover;
          // background-repeat: no-repeat;
          // width: 120rpx;
          // height: 50rpx;
          line-height: 50rpx;
          text {
            margin-left: 10rpx;
          }
        }
      }
      .head_rt {
        display: flex;
        flex-direction: row;
        font-size: 28rpx;
        align-items: center;
        color: #d19a66;
      }
      image {
        width: 50rpx;
        height: 50rpx;
      }
    }
    .news_center {
      margin-top: 10rpx;
      display: flex;
      flex-direction: row;
      align-items: flex-start;
      image {
        width: 250rpx;
        height: 200rpx;
      }
      .familyNews {
        margin-left: 20rpx;
        color: #d19a66;
        display: flex;
        flex-direction: row;
        align-items: flex-end;
        image {
          width: 50rpx;
          height: 50rpx;
          margin-right: 10rpx;
        }
      }
    }
    .news_bottom {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10rpx;
      color: #efa856;
      font-size: 30rpx;
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
  .ipt {
    margin-left: 15rpx;
  }
</style>
