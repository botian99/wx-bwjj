<template>
	<view class="login-content">
		<view class="logo-content">
			<img src="/static/baiwujinji.svg" alt="" class="logo-img" />
		</view>
		<view class="login-bars">
			<button class="wx-login" type="primary" lang="zh_CN" @click="login()">微信登录</button>
			<button class="custom-login" type="default" lang="zh_CN" @click="customToHome()">随便看看</button>
		</view>
		<view class="check-auth">
			<label>
				<checkbox class="round black" :value="checkAuth" @click="changeAuth()" />
			</label>
			<view class="check-auth-text">
				<text>我已阅读并同意《服务条款》和《隐私条款》</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				checkAuth: false
			}
		},
		methods: {
			changeAuth() {
				this.$data.checkAuth = !this.$data.checkAuth;
			},
			customToHome() {
				if (!this.$data.checkAuth) {
					uni.showToast({
						duration: 1000,
						icon: 'none',
						title: '请阅读并同意《服务条款》和《隐私条款》'
					});
					return;
				}
				this.goToHomePage();
			},
			login() {
				if (!this.$data.checkAuth) {
					uni.showToast({
						duration: 1000,
						icon: 'none',
						title: '请阅读并同意《服务条款》和《隐私条款》'
					});
					return;
				}
				// 登录
				uni.login({
				  provider: 'weixin',
				  success: res => {
				    console.log('微信登录成功', res);
				    if (res.code) {
				      // 获取到用户的登录凭证，可以发给后台进行用户信息获取
				      getUserInfo(res.code);
					  this.goToHomePage();
				    } else {
				      console.log('微信登录失败！');
				    }
				  },
				  fail: err => {
				    console.log('登录失败', err);
				  }
				});
				
				// 获取用户信息
				function getUserInfo(code) {
				  uni.request({
				    url: 'https://your-server.com/wechat-login', // 后台接口
				    method: 'POST',
				    data: {
				      code: code, // 传递微信登录凭证
				    },
				    success: res => {
				      console.log('获取用户信息成功', res);
				    },
				    fail: err => {
				      console.log('获取用户信息失败', err);
				    }
				  });
				}
			},
			goToHomePage(){
				console.log('goToHomePage');
				uni.navigateTo({
					url: '/pages/index/tabbar'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
.login-content {
	width: 100%;
	height: 100%;
	padding-top: 400rpx;
	color: #000;
	.logo-content {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 200rpx;
		margin-bottom: 400rpx;
		.logo-img {
			width: 53rpx;
			height: 200rpx;
		}
	}
	.login-bars {
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 0 30rpx;
		margin-bottom: 60rpx;
		button {
			width: 100%;
		}
		.wx-login {
			background-color: #1F2B38;
			margin-bottom: 20rpx;
		}
	}
	.check-auth {
		display: flex;
		justify-content: center;
		align-items: center;
		scale: 70%;
		.check-auth-text {
			margin-left: 10rpx;
		}
	}
}
</style>
