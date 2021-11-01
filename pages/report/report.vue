<template>
	<view class="report">
		<u-navbar :is-back="true" height="50" class="navbar" back-icon-color="#fff"   :background="background" :border-bottom="false">
			<view class="slot-wrap">
				<view class="title">
					{{title}}
				</view>
				<view class="icon">
					<view class="iconfont icon-guanbi"></view>
					<view class="iconfont icon-caozuo"></view>
				</view>
			</view>
		</u-navbar>
		<view class="container">
			<image class="apply"  src="../../static/reportNav.jpg" mode=""></image>
			<askForleave></askForleave>
			<u-button class="u-button"  :custom-style="customStyle" @click="navigateClearLeave">请假申请</u-button>
		</view>
	</view>
</template>

<script>
	import askForleave from "@/components/askForLeave.vue"
	import leave from "@/components/leave.vue"
	export default {
		components:{
			askForleave,
			leave
		},
		data() {
			return {
				background: {
					backgroundColor: '#6db0f7'
				},
				customStyle: {
					// marginTop: '20px', // 注意驼峰命名，并且值必须用引号包括，因为这是对象
					color: '#fff',
					backgroundColor: '#51aefe'
				},
				applyTop: 0,
				title:"学生外出报备"
			};
		},
		methods:{
			navigateClearLeave(){
				uni.navigateTo({
					url:"/pages/clearLeave/clearLeave"
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
		width: 200rpx;
		color: white;
		display: flex;
		align-items: center;
		.icon-caozuo{
			font-size: 60rpx;
			margin-left: 40rpx;
		}
	}
}
.report{
	position: relative;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	background: #f5f7f6;
	.container{
		.apply{
			width: 100%;
			height: 43px;
			object-fit: cover;
			position: fixed;
			left: 0;
			z-index: 999;
		}
		.u-button{
			position: fixed;
			bottom: 0;
			left: 0;
			width: 100%;
			height: 88rpx;
		}
	}
}


</style>
