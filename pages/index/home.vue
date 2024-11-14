<!-- 首页 -->
<template>
	<view>
		<cu-custom bgColor="bg-transparent" :isBack="false">
		</cu-custom>
		<view class="home-page-content">
			<image class="home-img" src="/static/home.png" alt=""></image>
			<view class="home-content">
				<view class="dianmao">
					点卯
				</view>
				<view class="right-time">
					<view class="time-top">
						甲子·甲子·甲子·甲子
					</view>
					<view class="time-bottom">
						农历9月20日
					</view>
				</view>
			</view>
			<view class="home-study">
				<view class="study-counter" @click="goToStudy()">
					<view class="study-text">
						学习
					</view>
					<text>10</text>
				</view>
				<view class="study-counter">
					<view class="study-text">
						复习
					</view>
					<text>1000</text>
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	import request from '@/common/request.js';
	export default {
		components: {

		},
		data() {
			return {
				tip: '点击「添加小程序」，下次访问更便捷',
				duration: 1,

				scrollTop: 0,
				old: {
					scrollTop: 0
				},

				bannerList: [{
						imageUrl: 'https://cdn.zhoukaiwen.com/zjx_banner.png'
					},
					{
						imageUrl: 'https://cdn.zhoukaiwen.com/zjx_banner3.png'
					},
					{
						imageUrl: 'https://cdn.zhoukaiwen.com/zjx_banner1.png'
					},
					{
						imageUrl: 'https://cdn.zhoukaiwen.com/zjx_banner2.png'
					}
				],
				categories: [{
						cuIcon: 'hotfill',
						color: 'red',
						badge: '优惠',
						mid: '1',
						name: '学习技术'
					},
					{
						cuIcon: 'colorlens',
						color: 'orange',
						badge: 1,
						mid: '2',
						name: '需求定制'
					},
					{
						cuIcon: 'goodsnewfill',
						color: 'yellow',
						badge: 12,
						mid: '3',
						name: '客户定制'
					},
					{
						cuIcon: 'calendar',
						color: 'cyan',
						badge: 22,
						mid: '4',
						name: '文章资讯'
					}
				],
				messageData: [{
						title: '「前端铺子」感谢大家的支持',
						tag: '感谢',
						content: '加群请在git上查看二维码或联系方式'
					},
					{
						title: '组件持续更新中，敬请期待！',
						tag: '更新',
						content: '致力提供优质的组件，gitee保持最新'
					}
				],
				curriculum: [{
						name: 'uniapp项目开发',
						content: 'uniapp小程序商城系统开发，实战项目...'
					},
					{
						name: '后台管理系统',
						content: 'vue+iview的后台管理系统建设系统开发...'
					},
					{
						name: 'App模板',
						content: '基于uniapp开发的效率类APP，开发至上线...'
					},
					{
						name: 'PC端官网开发',
						content: 'html/css/jQuery建设的PC端官方门户网站...'
					},
					{
						name: 'uniapp多端打包',
						content: 'uniapp开发完成上线的打包流程，上架商店等...'
					}
				],
				projectList: []
			};
		},
		watch: {},
		mounted() {
			console.log(this.projectList);
			this.getData();
			
			
			// 在页面中定义插屏广告
			let interstitialAd = null
			
			// 在页面onLoad回调事件中创建插屏广告实例
			if (wx.createInterstitialAd) {
			  interstitialAd = wx.createInterstitialAd({
			    adUnitId: 'adunit-0843cdd8084e561d'
			  })
			  interstitialAd.onLoad(() => {})
			  interstitialAd.onError((err) => {})
			  interstitialAd.onClose(() => {})
			}
			
			// 在适合的场景显示插屏广告
			if (interstitialAd) {
			  interstitialAd.show().catch((err) => {
			    console.error(err)
			  })
			}
			// 插屏广告结束
		},
		methods: {
			goToStudy() {
				uni.navigateTo({
					url: '/pages/knowledge/knowledge'
				})
			},
			getData() {
				console.log('数据加载');
				let opts = {
					url: 'api/project/list',
					method: 'get'
				};
				uni.showLoading({
					title: '加载中'
				});
				request.httpRequest(opts).then(res => {
					console.log(res);
					uni.hideLoading();
					if (res.statusCode == 200) {
						this.projectList = res.data.data;
					} else {
						this.projectList = [];
					}
				});
			},
			scroll: function(e) {
				console.log(e);
				this.old.scrollTop = e.detail.scrollTop;
			},
			goCategorieslist: function(e) {
				// console.log(e.currentTarget.dataset.mid)
				if (e.currentTarget.dataset.mid == 1 || e.currentTarget.dataset.mid == 2) {
					uni.navigateTo({
						url: '../timeline?mid=' + e.currentTarget.dataset.mid
					});
				} else if (e.currentTarget.dataset.mid == 3) {
					uni.navigateTo({
						url: '../../os_project/index'
					});
				} else if (e.currentTarget.dataset.mid == 4) {
					this.$emit('ShowNews', 'news')
					console.log('文章资讯')

				}
			},
			goProjectList() {
				uni.navigateTo({
					url: '../project/list'
				});
			},
			goProject(id) {
				uni.navigateTo({
					url: '../project/project?id=' + id
				});
			},
			goVideo() {
				uni.navigateTo({
					url: '../video'
				});
			},
			goAboutUs(){
				uni.navigateTo({
					url: '../me/about_us'
				})
			}
		},
		filters: {
			formatDate(value) {
				if (value == undefined) {
					return;
				}
				// let date = new Date(value * 1000);
				let date = new Date(value);
				//时间戳为10位需*1000，时间戳为13位的话不需乘1000
				let y = date.getFullYear();
				let MM = date.getMonth() + 1;
				MM = MM < 10 ? ('0' + MM) : MM; //月补0
				let d = date.getDate();
				d = d < 10 ? ('0' + d) : d; //天补0
				let h = date.getHours();
				h = h < 10 ? ('0' + h) : h; //小时补0
				let m = date.getMinutes();
				m = m < 10 ? ('0' + m) : m; //分钟补0
				let s = date.getSeconds();
				s = s < 10 ? ('0' + s) : s; //秒补0
				// return y + '-' + MM + '-' + d; //年月日	 + ' ' + h + ':' + m
				return y + '-' + MM + '-' + d; //年月日时分秒
			},
			typeF(value) {
				if (!value) {
					return;
				}
				if(value == 2){
					return 'Gitee开源'
				}
				if(value == 3){
					return '可商用'
				}
				if(value == 4){
					return '商业项目'
				}
				if(value == 5){
					return '付费模板'
				}
				if(value == 6){
					return '仅供参考'
				}
				if(value == 7){
					return '其他类型'
				}
			}
		},
	};
</script>
<style lang="scss" scoped>
	.home-page-content {
		padding: 0 30px;
		.home-img {
			width: 100%;
			height: 440px;
		}
		.home-content {
			margin-top: 15px;
			padding: 17px 20px;
			display: flex;
			justify-content: space-between;
			align-items: center;
			width: 100%;
			height: 72px;
			background-color: #FFFFFF;
			.dianmao {
				font-size: 18px;
				font-weight: 600;
			}
			.right-time {
				display: flex;
				flex-direction: column;
				justify-content: space-between;
				align-items: flex-end;
				.time-top {
					font-size: 11px;
					font-family: PingFang SC;
					color: #8095AA;
				}
				.time-bottom {
					font-family: Source Han Serif SC VF;
					font-size: 16px;
					font-weight: 500;
				}
			}
		}
		.home-study {
			width: 100%;
			height: 72px;
			margin-top: 15px;
			display: flex;
			justify-content: space-between;
			align-items: center;
			.study-counter {
				width: 150px;
				height: 100%;
				background-color: #FFFFFF;
				padding: 15px 20px;
				flex-direction: column;
				justify-content: space-between;
				align-items: center;
				text {
					font-size: 18px;
					font-family: PingFang SC;
					color: #1F2B38;
					font-weight: 600;
				}
				.study-text {
					font-size: 11px;
					font-family: PingFang SC;
					color: #8095AA;
					
				}
				
			}
		}

	}

	.swiper-box {
		flex: 1;
	}

	.swiper-item {
		height: 100%;
	}
	.jn_img{
		width: 700rpx;
		display: block;
		margin: 15rpx auto;
		border-radius: 20rpx;
	}

	.message-box {
		width: 100%;
		height: 120rpx;
		background: url(https://zhoukaiwen.com/img/icon/clock.gif) #FFFFFF;
		background-repeat: no-repeat;
		background-size: 100rpx 100rpx;
		background-position: 15rpx 10rpx;
		margin: 0rpx 0rpx 10rpx 0rpx;
		padding-left: 130rpx;

		.message-tltle {
			height: 65rpx;
			line-height: 70rpx;
			font-weight: 600;
			font-size: 28rpx;
		}

		.message-content {
			color: #0081ff;

			span {
				background-color: #0081ff;
				color: #FFFFFF;
				padding: 2rpx 8rpx;
				border-radius: 8rpx;
				margin-right: 8rpx;
			}
		}
	}

	/*scroll-view外层*/
	.skill-sequence-panel-content-wrapper {
		position: relative;
		white-space: nowrap;
		padding: 10rpx 0 10rpx 10rpx;
	}

	/*左右渐变遮罩*/
	.hide-content-box {
		position: absolute;
		top: 0;
		height: 100%;
		width: 10px;
		z-index: 2;
	}

	.hide-content-box-left {
		left: 0;
		background-image: linear-gradient(to left, rgba(255, 255, 255, 0), #f3f3f3 60%);
	}

	.hide-content-box-right {
		right: 0;
		background-image: linear-gradient(to right, rgba(255, 255, 255, 0), #f3f3f3 60%);
	}

	.kite-classify-scroll {
		width: 100%;
		height: 380rpx;
		overflow: hidden;
		white-space: nowrap;
	}

	.kite-classify-cell {
		display: inline-block;
		width: 266rpx;
		height: 370rpx;
		margin-right: 20rpx;
		background-color: #ffffff;
		border-radius: 10rpx;
		overflow: hidden;
		box-shadow: 2px 2px 3px rgba(26, 26, 26, 0.2);
	}

	.nav-li {
		padding: 40rpx 30rpx;
		width: 100%;
		background-image: url(https://s1.ax1x.com/2020/06/27/NyU04x.png);
		background-size: cover;
		background-position: center;
		position: relative;
		z-index: 1;
	}

	.nav-name {
		font-size: 28upx;
		text-transform: Capitalize;
		margin-top: 20upx;
		position: relative;
	}

	.nav-name::before {
		content: '';
		position: absolute;
		display: block;
		width: 40rpx;
		height: 6rpx;
		background: #fff;
		bottom: 0;
		right: 0;
		opacity: 0.5;
	}

	.nav-name::after {
		content: '';
		position: absolute;
		display: block;
		width: 100rpx;
		height: 1px;
		background: #fff;
		bottom: 0;
		right: 40rpx;
		opacity: 0.3;
	}

	.nav-content {
		width: 100%;
		padding: 15rpx;
		display: inline-block;
		overflow-wrap: break-word;
		white-space: normal;
	}

	.nav-btn {
		width: 200rpx;
		height: 60rpx;
		margin: 8rpx auto;
		text-align: center;
		line-height: 60rpx;
		border-radius: 10rpx;
	}

	.bg-index1 {
		background-color: #19cf8a;
		color: #fff;
	}

	.bg-index2 {
		background-color: #954ff6;
		color: #fff;
	}

	.bg-index3 {
		background-color: #5177ee;
		color: #fff;
	}

	.bg-index4 {
		background-color: #f49a02;
		color: #fff;
	}

	.bg-index5 {
		background-color: #ff4f94;
		color: #fff;
	}

	.bg-index6 {
		background-color: #7fd02b;
		color: #fff;
	}

	.item-name {
		margin-bottom: 15rpx;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 1;
		overflow: hidden;
	}
</style>
