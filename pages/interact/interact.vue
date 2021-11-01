<template>
	<view>
		<view style="width: 100%; height: 50rpx; background-color: #6cb0f9;">1</view>
		<image src="../../static/tabbar2.jpg" mode="" style="width: 100%; height: 1150px; object-fit: cover;"></image>
		<u-tabbar v-model="current" icon-size='60' active-color="#8dc9ff" height="110" :list="list" :mid-button="true"></u-tabbar>
	</view>
</template>

<script>
	import {tabbar} from "@/util/common.js";
	export default {
		data() {
			return {
				background: {
					backgroundColor: '#6db0f7'
				},
				list:tabbar,
				current: 0
			};
		}
	}
</script>

<style lang="scss">
</style>
