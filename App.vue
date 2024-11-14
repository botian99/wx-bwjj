<script>
	import Vue from 'vue'
	export default {
		onLaunch: function() {
			uni.getSystemInfo({
				success: function(e) {
					// #ifndef MP
					Vue.prototype.StatusBar = e.statusBarHeight;
					if (e.platform == 'android') {
						Vue.prototype.CustomBar = e.statusBarHeight + 50;
					} else {
						Vue.prototype.CustomBar = e.statusBarHeight + 45;
					};
					// #endif

					// #ifdef MP-WEIXIN
					Vue.prototype.StatusBar = e.statusBarHeight;
					let custom = wx.getMenuButtonBoundingClientRect();
					Vue.prototype.Custom = custom;
					Vue.prototype.CustomBar = custom.bottom + custom.top - e.statusBarHeight + 4;
					// #endif		

					// #ifdef MP-ALIPAY
					Vue.prototype.StatusBar = e.statusBarHeight;
					Vue.prototype.CustomBar = e.statusBarHeight + e.titleBarHeight;
					// #endif
				}
			});
		},
		onShow: function() {
			console.log('App Show');
			// 检查用户是否已授权
			uni.getSetting({
			  success(res) {
			    if (!res.authSetting['scope.userInfo']) {
			      // 用户未授权，主动引导授权
			      uni.authorize({
			        scope: 'scope.userInfo', // 需要的权限
			        success() {
			          console.log('用户授权成功');
			          // 授权成功后可以获取用户信息
			          uni.getUserInfo({
			            success(userInfoRes) {
			              console.log('用户信息', userInfoRes.userInfo);
			            },
			            fail(err) {
			              console.log('获取用户信息失败', err);
			            }
			          });
			        },
			        fail() {
			          console.log('用户拒绝授权');
			          // 用户拒绝授权时，可以提示用户去设置页修改授权
			          uni.openSetting({
			            success(settingRes) {
			              if (settingRes.authSetting['scope.userInfo']) {
			                console.log('用户已授权');
			              } else {
			                console.log('用户仍未授权');
			              }
			            }
			          });
			        }
			      });
			    } else {
			      console.log('用户已经授权');
			      // 可以直接获取用户信息
			      uni.getUserInfo({
			        success(userInfoRes) {
			          console.log('用户信息', userInfoRes.userInfo);
			        }
			      });
			    }
			  }
			});

		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	@import "colorui/main.css";
	@import "colorui/icon.css";
	@import "uview-ui/index.scss";
</style>
