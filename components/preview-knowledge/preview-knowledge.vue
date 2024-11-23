<template>
	<view class="knowledge-preview-content">
		<view class="knowledge-info">
			<view class="info-title">
				<view class="info-title-text">
					{{title}}
				</view>
				<view class="info-status" v-show="isStudyNow">
					正在学习
				</view>
			</view>
			<view class="info-abstract">
				{{abstract}}
			</view>
			<view class="info-count">
				{{knowledgeCount}}个知识点
			</view>
		</view>
		<view class="knowledge-image">
			<image src="/static/knowledge/knowledge-item.svg" mode="" :lazy-load="true"></image>
		</view>
	</view>
</template>

<script>
	export default {
		name: "preview-knowledge",
		data() {
			return {

			};
		},
		props: {
			title: {
				type: String,
				default: ''
			},
			isStudyNow: {
				type: Boolean,
				default: false
			},
			abstract: { // 摘要
				type: String,
				default: ''
			},
			knowledgeImage: {
				type: String,
				default: ''
			},
			knowledgeCount: {
				type: Number,
				default: 0,
			}
		},
	}
</script>

<style lang="scss">
	.knowledge-preview-content {
		width: 750rpx;
		height: 300rpx;
		padding: 30rpx 60rpx;
		display: flex;
		flex-direction: row;
		.knowledge-image image {
			width: 180rpx;
			height: 240rpx;
		}
		.knowledge-info {
			flex-grow: 1;
			display: flex;
			flex-direction: column;
			padding-right: 30rpx;
			.info-title {
				display: flex;
				flex-direction: row;
				align-items: center;
				margin-bottom: 16rpx;
				.info-title-text {
					font-size: 36rpx;
					font-weight: 600;
					line-height: 40rpx;
					margin-right: 8rpx;
				}
				.info-status {
					background-color: #F7FAFD;
					border-radius: 8rpx;
					padding: 6rpx 20rpx;
					font-size: 22rpx;
				}
			}
			.info-abstract {
				flex-grow: 1;
				font-family: PingFang SC;
				font-size: 22rpx;
				line-height: 40rpx;
				font-weight: 400;
				color: #475665;
			}
			.info-count {
				font-family: PingFang SC;
				font-size: 22rpx;
				line-height: 40rpx;
				font-weight: 400;
				color: #8095AA;
			}
		}
	}
</style>