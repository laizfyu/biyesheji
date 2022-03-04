<template>
  <view>
    <view class="family_name">
      <text>家庭名称:</text>
      <u-input 
        v-model="familyName" 
        type="text" 
        border="true" 
        border-color="#FF9900"
        placeholder="最长可输入10个字符"
        maxlength="10"/>
    </view> 
    <view class="add_member">
      <image src="/static/iconfont/addFamilyUser.png" mode=""></image>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        familyName: ""
      }
    },
    methods: {
      
    }
  }
</script>

<style lang="scss">
  .family_name {
    display: flex;
    flex-direction: row;
    align-items: center;
    height: 100rpx;
    line-height: 90rpx;
    border-bottom: solid 2rpx #bababa;
    margin: 20rpx;
    text {
      margin-right: 10rpx;
      font-size: 30rpx;
      font-weight: 500;
    }
  }
  .add_member {
    
  }
</style>
