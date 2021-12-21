<template>
  <view>
    
    <view class="family_item">
      <text>家庭标签:</text>
      <text style="color: #FF9900;">FY0001</text>
    </view>
    <!-- 修改家庭名称 -->
    <view class="family_item">
      <text>家庭名称:</text>
      <view class="rt" @click="getNameShow">
        <text>{{familyName}}</text> 
        <image src="../../static/iconfont/arrow-right.png" mode=""></image>
      </view>
    </view>
    <u-modal
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
    </u-modal>
    <!-- 修改家庭头像 -->
    <view class="family_item">
      <text>家庭头像:</text>
      <view class="rt" @click="getFamilyImg">
        <image src="../../static/iconfont/arrow-right.png" mode=""></image>
      </view>
    </view>
    <view class="familyImg">
      <image src="../../static/img/jiaju.webp" mode="aspectFit"></image>
    </view>
    <!-- 家庭成员模块 -->
    <view class="family_member">
      <u-collapse>
      		<u-collapse-item title="家庭成员:">
            <view class="member">
              <text>小明</text>
              <text>108806</text>
            </view>
            <view class="member">
              <text>小红</text>
              <text>101865</text>
            </view>
            <view class="member">
              <text>小华</text>
              <text>108080</text>
            </view>
            <view class="member">
              <text>小张</text>
              <text>145061</text>
            </view>
            <view class="member">
              <text>小小</text>
              <text>108806</text>
            </view>
            <view class="member">
              <text>小于</text>
              <text>108806</text>
            </view>
            <view class="member">
              <text>小巫</text>
              <text>108806</text>
            </view>
            <view class="member">
              <text>小哈</text>
              <text>108806</text>
            </view>
            <view class="addBtn">
              <image src="../../static/iconfont/add_shouna.png" mode=""></image>
              <text>添加成员</text>
            </view>
      		</u-collapse-item>
          <!-- 底部保存按钮 -->
          <button type="default" class="buttom">确认修改</button>
      	</u-collapse>
    </view>
    <!-- 底部保存按钮 -->
    <!-- <button type="default" class="buttom">确认修改</button> -->
    <!-- 操作提示 -->
    <u-toast ref="uToast" />
  </view>
</template>

<script>
  export default {
    data() {
      return {
        nameShow: false,
        familyName: "小明的一家"
      }
    },
    methods: {
      // 跳转到头像修改页面
      getFamilyImg() {
        uni.navigateTo({
          url: "../familyImg/familyImg"
        })
      },
      // 弹出家庭名称修改框
      getNameShow() {
        this.nameShow = true
      },
      setModal() {
        if (this.value.length === 0) {
          console.log("不能为空",this.name)
          this.$refs.uToast.show({
            title: '家庭名称不能为空',
            type: 'warning',
          })
        } else {
          this.familyName = this.value
        }
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
