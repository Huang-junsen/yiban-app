<template>
	<view class="reportList">
		<image class="apply"  src="../static/reportNav.jpg" mode=""></image>
		<view style="width: 750rpx; height: 43px;"></view>
		<slot></slot>
		<view style="width: 750rpx; height: 88rpx;"></view>
		<u-button class="u-button" :custom-style="customStyle">请假申请</u-button>
	</view>
</template>


<script>
	
	export default {
		name:"reportList",
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss">
.reportList{
	width: 750rpx;
	background-color: #f5f7f6;
	position: fixed;
	left: 0;
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
</style>
