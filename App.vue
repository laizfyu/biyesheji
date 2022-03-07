<script>
	export default {
    // 定义全局接口地址
    globalData:{
      domain : "http://aff83e9.cpolar.cn/api",
    },
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			// wx.getUserProfile({
			//   lang: "zh_CN",
			//   desc: "登录",
			//   success: (res) => {
			//     // console.log(res),
			//     const userName = res.userInfo.nickName;
          // console.log(userName);
			      wx.login({
			        success: (open) => {
                console.log("发送请求");
			          console.log(open);
			          console.log("code:" + open.code);
			          //发起网络请求,获取openid
			          wx.request({
			            url: "http://aff83e9.cpolar.cn/api/wxlogin",
			            data: {
			              code: open.code,
			            },
			            method: "POST",
			            success: (r) => {
			              // console.log("用户的openid:" + r.data.data.openid);
                    console.log(r);
			             if(r.data.data) {
                      wx.setStorageSync("userInfo", r.data.data);
                      // wx.reLaunch({
                      //   url: "pages/index/index"
                      // })
                   } else {
                     wx.reLaunch({
                       url: "/pages/login/login"
                     })
                   }
			            },
			            fail: (error) => {
			              console.log(error);
			            },
			          })
			        }
			      });
			  },
			  // fail: (err) => {
			  //   console.log(err)
			  // }
			// })
		// },
		onHide: function() {
			console.log('App Hide')
		},
    
	}
</script>

<style lang="scss">
  @import "uview-ui/index.scss";
	/*每个页面公共css */
</style> 
