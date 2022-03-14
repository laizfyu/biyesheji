<template>
  <view>
    <view class="search">
      <view class="search_lf">
        <u-search
        placeholder="输入分类 名称 盒子 家庭进行检索" 
        v-model="keyword"
        shape="round"
        :clearabled="true"
        :showAction="false"
        @search="getList()">
        </u-search>
      </view>
      <view class="btm" @click="getList()">搜索</view>
    </view>
    
    <view class="shouna_item" v-for="(item,index) in list" :key="item.index" @click="getWupin(index)">
      <view class="item_head">
        <view class="head_lf">
          <image src="/static/iconfont/add_item.png" mode=""></image>
          <text>{{item.wupinId}}</text>
        </view>
        <text class="head_rt">{{item.wupinName}}</text>
      </view>
      <view class="item_center">
        <image :src="item.wupinImg" mode="aspectFit"></image>
        <!-- {{item.wupinImg}} -->
        <view class="center_show"><text>描述:</text>{{item.wupinMiaoshu}}</view>
      </view>
      <view class="item_bottom">
        <view>{{item.wupinTime}}</view>
        <view><text>¥ {{item.wupinPic}}</text> <text>x {{item.wupinNum}}</text></view>
      </view>
    </view>
    
  </view>
</template>

<script>
  const app = getApp()
  const domain = app.globalData.domain
  export default {
    data() {
      return {
        keyword: '', //搜索条件
        list: "", //物品列表
        user_id: "", //用户id
      }
    },
    methods: {
      getList() {
        const users = uni.getStorageSync("userInfo");
        console.log("用户信息:")
        console.log(users);
        this.user_id = users.id;
        wx.request({
          url: domain + "/list",
          method: "POST" ,
          data: {
            userId: this.user_id,
            queryParam: this.keyword
          },
          success:(res) => {
            console.log(res)
            this.list = res.data.data;
            console.log(this.list)
          }
        })
      },
      getWupin(index) {
        let boxId = this.list[index].id;
        uni.navigateTo({
          url: "/pagesB/wupin_detail/wupin_detail?boxId=" + boxId
        }) 
      }
    }
  }
</script>

<style lang="scss">
.search {
  width: 688rpx;
  margin: 20rpx auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .search_lf {
    width: 600rpx;
  }
  .btm {
    width: 100rpx;
    height: 60rpx;
    background-color: #ffaa00;
    color: #fff;
    line-height: 60rpx;
    text-align: center;
    border-radius: 30rpx;
    margin-left: 20rpx;
  }
}
.shouna_item {
     margin: 30rpx auto 0;
     padding-bottom: 20rpx;
     width: 688rpx;
     min-height: 328rpx;
     box-shadow: 0px 1rpx 11rpx 2rpx rgba(98, 98, 98, 0.1);
     border-radius: 8rpx;
     .item_head {
       display: flex;
       justify-content: space-between;
       .head_lf {
         display: flex;
         align-items: center;
         image {
           width: 80rpx;
           height: 80rpx;
           margin-top: -10rpx;
         }
       }
       .head_rt {
         margin: 15rpx 20rpx 0 0;
       }
     }
     .item_center {
       margin: 20rpx 20rpx 0 20rpx;
       display: flex;
       flex-direction: row;
       image {
         width: 170rpx;
         height: 170rpx;
       }
       .center_show {
         width: 480rpx;
         height: 170rpx;
         // padding-top: 10rpx;
         margin-left: 12rpx;
         font-size: 25rpx;
         color: #8c8c8c;
         display: -webkit-box;
         -webkit-box-orient: vertical;
         -webkit-line-clamp: 4;
         overflow: hidden;
         text {
           font-size: 30rpx;
           font-weight: 500;
           color: #000000;
         }
       }
     }
     .item_bottom {
       display: flex;
       justify-content: space-between;
       padding: 0 20rpx;
       margin-top: 20rpx;
       text {
         margin-right: 10rpx;
       }
     }
    }
</style>
