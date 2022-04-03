<template>
	<view>
		<u-navbar :is-back="true" back-icon-color="#fff"   :background="background" :border-bottom="false">
			<view class="slot-wrap">
				<view class="title">
					广州科技贸易职业学院
				</view>
				<view class="icon">
					<view class="iconfont icon-caozuo"></view>
				</view>
			</view>
		</u-navbar>
		<view class="xiaobenhua">
			<image src="../../static/xiaobenhua.jpg" mode=""></image>
			<view class="report" @click="report"></view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				background: {
					backgroundColor: '#6db0f7'
				},
			};
		},
		methods:{
			report(){
				uni.navigateTo({
					url:'/pages/report/report'
				})
			}
		}
	}
</script>

<style lang="scss">
.slot-wrap{
		width: 750rpx;
		display: flex;
		justify-content: space-between;
		padding-left: 20rpx;
		padding-right: 20rpx;
		align-items: center;
		.title{
			color: white;
			font-size: 32rpx;
			font-weight: bold;
		}
		.icon{
			width: 140rpx;
			color: white;
			.icon-caozuo{
				font-size: 60rpx;
			}
		}
	}
.xiaobenhua{
	width: 100%;
	position: relative;
	image{
		width: 100%;
		height: 753px;
	}
	.report{
		width: 150rpx;
		height: 120rpx;
		position: absolute;
		right: 390rpx;
		top: 510rpx;
	}
	
}
</style>
