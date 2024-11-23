<template>
	<view class="tabbar_container">
		<home @ShowNews="ShowNews" v-if="PageCur=='home'"></home>
		<search v-if="PageCur=='search'"></search>
		<cases v-if="PageCur=='cases'"></cases>
		<news v-if="PageCur=='news'"></news>
		<me v-if="PageCur=='me'"></me>
		<view class="tabbar_box">
				<view class="icon_tabbar">
					<image src="../../static/tabBar/home_bar.svg" @tap="openKnowledgeList"></image>
				</view>
				<view class="icon_tabbar">
					<image src="../../static/tabBar/point_bar.svg"></image>
				</view>
				<view class="icon_tabbar">
					<image src="../../static/tabBar/collection_bar.svg"></image>
				</view>
				<view class="icon_tabbar">
					<image src="../../static/tabBar/calendar_bar.svg"></image>
				</view>
		</view>
	</view>
</template>

<script>
	import request from '@/common/request.js';
	import home from "./home.vue";	//首页
	import search from "./search.vue";	//技术视频
	import cases from "./main.vue";	//宅家学
	import news from "./news.vue";	//资讯
	import me from "./me.vue";	//个人中心
	export default {
		components: {
			home,
			search,
			cases,
			news,
			me
		},
		data() {
			return {
				PageCur: 'home',
				message: '0',
				openId:'',
				access_token:'',
				tip:"我是提示",
				duration:1

			};
		},
		// 分享小程序
		onShareAppMessage(res) {
			return {
				title: '学技术·找案例，快来「前端铺子」吧！',
				imageUrl: 'https://cdn.zhoukaiwen.com/qdpz_share.jpg',
			};
		},
		onLoad(option){
			console.log('来自页面:', option)
			wx.showShareMenu({
				withShareTicket: true
			})
			if (option.type == 'matting') {
				uni.navigateTo({
					url: '../main/matting'
				})
				return
			}
		},
		onShareTimeline() {
			return {
				title: '学技术·找案例，快来「前端铺子」吧！',
			}
		},
		onShow() {
			this.getData();
		},
		methods: {
			getData() {
				let opts = {
					url: 'api/blog/list',
					method: 'get'
				};
				uni.showLoading({
					title: '加载中'
				});
				request.httpRequest(opts).then(res => {
					// console.log(res);
					uni.hideLoading();
					if (res.statusCode == 200) {
						this.message = res.data.data.length;
					} else {
						console.log('数据请求错误～');
					}
				});
			},
			ShowNews(e){
				console.log(e)
				this.PageCur = e;
			},
			NavChange: function(e) {
				console.log(e.currentTarget.dataset.cur)

				this.PageCur = e.currentTarget.dataset.cur;

				if (this.PageCur == 'index') {
					// document.title = '首页'
				} else if (this.PageCur == 'component') {
					// document.title = '积分商城'
				} else if (this.PageCur == 'cases') {
					// document.title = '宅家学'
				} else if (this.PageCur == 'news') {
					// document.title = '文章资讯'
				} else if (this.PageCur == 'me') {
					// document.title = '个人中心'
				}

				// uni.setStorage({
				// 	key: 'PageCur',
				// 	data: this.PageCur,
				// 	success: function() {
				// 		console.log('保存成功！');
				// 	}
				// });
			},
			NavChange_xd: function() {
				uni.navigateTo({
					url: 'publish',
					animationType: 'slide-in-bottom',
					animationDuration: 200
				});
			},
			openKnowledgeList() {
				uni.navigateTo({
					url: '/pages/knowledge/knowledgeList'
				})
			}
		}
	}
</script>

<style lang="scss">
	.tabbar_container {
		position: relative;
		height: 100vh;
		width: 100vw;
	}
	.color_main{
		color: #000000;
		font-weight: 900;
	}
	.tabbar_content_box {
		height: 0;
		flex-grow: 1;
	}
	.tabbar_box {
		position: absolute;
		bottom: 0;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
		margin-bottom: 50px;
		margin-top: 26px;
		width: 100vw;
		height: 24px;
		.icon_tabbar image{
			width: 24px;
			height: 24px;
		}
	}
</style>
