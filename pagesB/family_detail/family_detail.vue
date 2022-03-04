<template>
  <view>
    
    <view class="family_item">
      <text>家庭标签:</text>
      <text style="color: #FF9900;">{{familyId}}</text>
    </view>
    <!-- 修改家庭名称 -->
    <view class="family_item">
      <text>家庭名称:</text>
      <view class="rt">
        <text>{{familyName}}</text> 
        <!-- <image src="../../static/iconfont/arrow-right.png" mode=""></image> -->
      </view>
    </view>
   <!-- <u-modal
      show-cancel-button 
      v-model="nameShow" 
      title="请输入家庭名称" 
      @confirm="setModal" 
      confirm-color="#dea36c">
      <view class="slot-content">
        <view class="ipt">
          <u-input v-model="value" type=text focus maxlength=10 />
        </view>
      </view>
    </u-modal> -->
    <!-- 修改家庭头像 -->
    <!-- <view class="family_item">
      <text>家庭头像:</text>
      <view class="rt" @click="getFamilyImg">
        <image src="../../static/iconfont/arrow-right.png" mode=""></image>
      </view>
    </view>
    <view class="familyImg">
      <image src="../../static/img/jiaju.webp" mode="aspectFit"></image>
    </view> -->
    <!-- 家庭成员模块 -->
    <view class="family_member">
      <u-collapse>
      		<u-collapse-item title="家庭成员:">
            <view class="member" v-for="(item,index) in familyUser" :key="item.index">
              <text>{{item.userName}}</text>
              <text>{{item.userPhone}}</text>
            </view>
            <view class="addBtn" @click="getShow()">
              <image src="../../static/iconfont/add_shouna.png" mode=""></image>
              <text>添加成员</text>
            </view>
      		</u-collapse-item>
          <!-- 底部保存按钮 -->
          <!-- <button type="default" class="buttom">确认修改</button> -->
      	</u-collapse>
        <u-modal
          show-cancel-button 
          v-model="show" 
          title="请输入成员电话号码" 
          @confirm="setModal" 
          confirm-color="#dea36c">
          <view class="slot-content">
            <view class="ipt">
              <u-input v-model="phone" type=text focus maxlength=11 />
            </view>
          </view>
        </u-modal>
    </view>
    <!-- 底部保存按钮 -->
    <!-- <button type="default" class="buttom">确认修改</button> -->
    <!-- 操作提示 -->
    <u-toast ref="uToast" />
  </view>
</template>

<script>
  const app = getApp()
  const domain = app.globalData.domain
  export default {
    data() {
      return {
        nameShow: false,
        familyName: "小明的一家",
        familyDetail: "",
        familyId: "",
        show: false,
        phone: "",
        familyUser: ""
      }
    },
    onLoad(options) {
      this.familyDetail = JSON.parse(decodeURIComponent(options.detail));
      this.familyName = this.familyDetail.familyName;
      this.familyId = this.familyDetail.familyId;
    },
    onShow() {
      this.getFamilyUser()
    },
    methods: {
      getFamilyUser() {
        wx.request({
          url: domain + "/getUsersByFamilyId?familyId=" + this.familyId,
          method: "GET",
          success:(rrr) => {
            console.log(rrr)
            this.familyUser = rrr.data.data
          }
        })
      },
      // // 跳转到头像修改页面
      // getFamilyImg() {
      //   uni.navigateTo({
      //     url: "../familyImg/familyImg"
      //   })
      // },
      // 弹出添加成员框
      getShow() {
        this.show = true
      },
      setModal() {
        wx.request({
          url: domain + "/addFamilyUser",
          data: {
            userPhone: this.phone,
            familyId: this.familyId,
            familyName: this.familyName
          },
          method: "POST",
          success:(res) => {
            console.log(res)
            this.$refs.uToast.show({
              title: res.data.msg,
              type: 'warning',
            })
            setTimeout(() => {
              this.getFamilyUser()
            }, 1000); 
          }
        })
      }
    }
  }
</script>

<style lang="scss">
  .family_item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: solid 2rpx #F0AD4E;
    margin: 20rpx;
    // padding-bottom: 10rpx;
    height: 80rpx;
    line-height: 80rpx;
  }
  .rt {
    display: flex;
    align-items: center;
    color: #FF9900;
    image {
      width: 36rpx;
      height: 36rpx;
      margin-left: 10rpx;
    }
  }
  .familyImg {
    width: 300rpx;
    height: 300rpx;
    margin: 20rpx auto;
    image {
      width: 100%;
      height: 100%;
    }
  }
  .family_member {
    margin: 20rpx;
    border-bottom: solid 2rpx #F0AD4E;
    height: 80rpx;
    line-height: 80rpx;
    .member {
      display: flex;
      justify-content: space-between;
    }
  }
  .addBtn {
    width: 682rpx;
    height: 84rpx;
    background: #F5F5F5;
    border-radius: 12rpx;
    display: flex;
    align-items: center;
    justify-content: center;
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
  .buttom {
    width: 640rpx;
    height: 84rpx;
    margin: 100rpx auto;
    background-color: #e19d3e !important;
  }
  .ipt {
    padding: 10rpx 20rpx;
  }
</style>
