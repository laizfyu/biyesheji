<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},
    // 定义全局接口地址
    globalData:{
      domain : "http://12a49c46.cpolar.io/api",
    }
	}
</script>

<style lang="scss">
  @import "uview-ui/index.scss";
	/*每个页面公共css */
</style>
