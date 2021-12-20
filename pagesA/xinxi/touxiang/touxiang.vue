<template>
  <view class="touxiang">
    <u-top-tips ref="uTips"></u-top-tips>
    <image :src="img" mode="aspectFit" @click="changImg()"></image>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        img: "../../../static/img/touxiang.jpg"
      }
    },
    methods: {
      // 更改头像
      changImg() {
        uni.chooseImage({
          count: 1,
          //调用成功则返回图片的本地文件路径列表 tempFilePaths
          success: res => {
            this.img = res.tempFilePaths,
            this.$refs.uTips.show({
              title: '头像更换成功',
              type: 'error',
              duration: '2300'
            })
          },
          // 调用失败返回
          fail() {
            this.$refs.uTips.show({
              title: '更改头像失败',
              type: 'error',
              duration: '2300'
            })
          },
          // 调用结束返回上一个页面
          complete() {
            uni.navigateBack({
              delta: 1,
            })
          }
        })
      }
    }
  }
</script>

<style lang="scss">
  page {
    height: 100%;
  }

  .touxiang {
    display: flex;
    height: 100%;
    background-color: #333;
    justify-content: center;
    /*水平居中*/
    align-items: center;

    /*垂直居中*/
    image {
      width: 100%;
    }
  }
</style>
