<template>
	<view class="knowledge-list-content">
		<cu-custom bgColor="bg-white" :isBack="true">
			<block slot="content">知识库</block>
		</cu-custom>
		<u-tabs :list="list1" @click="click" :scrollable="false" :activeStyle="{
            color: '#1F2B38',
            fontWeight: 'bold',
        }" lineColor="#1F2B38" :inactiveStyle="{
            color: '#8095AA',
            transform: 'scale(1)'
        }"></u-tabs>
		<view class="btns-list">
			<button class="dv-tabs-btn" v-for="(item,index) in btns" :key="item.name"
				:class="{selected: item.name === selectsubKnowledge}"
				@tap="onSelectsubKnowledge(item)">{{item.name}}</button>
		</view>
		<view class="knowledge-list-view" v-for="(item,index) in knowledgeList" :key="`${item.name}_${index}`">
			<preview-knowledge :abstract="item.abstract" :is-study-now="item.isStudyNow" :title="item.title"
				:knowledge-count="item.knowledgeCount" :knowledge-image="item.knowledgeImage"></preview-knowledge>
		</view>
		<view style="font-size: 22rpx;line-height: 32rpx;text-align: center;color: #8095AA;margin-bottom: 20rpx;">
			没有找到想学的知识库？
		</view>
		<button class="get-more-btn" shape="circle">了解如何自制知识库</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				selectsubKnowledge: '',
				list1: [{
					name: '山',
				}, {
					name: '医',
				}, {
					name: '命'
				}, {
					name: '相'
				}, {
					name: '卜'
				}],
				btns: [{
					name: '面相'
				}, {
					name: '手相'
				}, {
					name: '风水学'
				}, {
					name: '姓名学'
				}],
				knowledgeList: [{
					title: '麻衣神相',
					abstract: '中国古代对人体相貌进行系统叙述的相术著作，由北宋人李和弟子陈抟所撰,奠定了相...',
					knowledgeImage: '',
					isStudyNow: true,
					knowledgeCount: 1000,
				}, {
					title: '麻衣神相',
					abstract: '中国古代对人体相貌进行系统叙述的相术著作，由北宋人李和弟子陈抟所撰,奠定了相...',
					knowledgeImage: '',
					isStudyNow: false,
					knowledgeCount: 1000,
				}, {
					title: '麻衣神相',
					abstract: '中国古代对人体相貌进行系统叙述的相术著作，由北宋人李和弟子陈抟所撰,奠定了相...',
					knowledgeImage: '',
					isStudyNow: false,
					knowledgeCount: 1000,
				}]
			}
		},
		methods: {
			click(item) {
				console.log('item', item);
			},
			onSelectsubKnowledge(item) {
				console.log('item', item.name);
				this.selectsubKnowledge = item.name;
				console.log('selectsubKnowledge', this.selectsubKnowledge);
			}
		}
	}
</script>

<style lang="scss">
	.knowledge-list-content {
		background-color: #FFFFFF;
		width: 100vw;
		height: 100vh;
		display: flex;
		flex-direction: column;

		.btns-list {
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			padding: 30rpx 60rpx;
		}
	}

	.dv-tabs-btn {
		background-color: #F7FAFD;
		border-radius: 40rpx;
		height: 56rpx;
		padding: 8rpx 40rpx;
		color: #8095AA;
		font-size: 22rpx;
		line-height: 40rpx;
		border: 0px solid transparent;

		&.selected {
			background-color: #1F2B38;
			color: #FFFFFF;
		}

		&::after {
			border: 0px solid transparent;
		}
	}
	.get-more-btn {
		font-size: 22rpx;
		line-height: 40rpx;
		padding: 12rpx 16rpx;
		background-color: #FFFFFF;
		color: #475665;
		width: 230rpx;
		border: 1px solid #F0F5FA;
		border-radius: 34rpx;
		box-sizing: border-box;
		&::after {
		border-radius: 34rpx;
		border: 1px solid #F0F5FA;
		}
		
	}
</style>