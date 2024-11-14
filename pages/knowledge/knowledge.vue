<template>
	<view class="container">
		<view class="glass-effect">
			<image src="../../static/home.png" mode=""></image>
			<text>毛玻璃效果的文本</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {

		}
	}
</script>

<style lang="scss">
	.container {
		position: relative;
		display: flex;
		width: 100%;
		height: 100%;
		background-size: cover;
		filter: blur(10px);
	}
	.glass-effect {
		width: 100%;
		height: 100%;
		/* 半透明背景 */
		display: flex;
		justify-content: center;
		align-items: center;
		color: #fff;
		font-size: 20px;
		text-align: center;
		image {
			position: absolute;
			left: 0;
			right: 0;
			top: 0;
			bottom: 0;
			
		}
	}
</style>