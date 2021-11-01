<template>
	<view>
		<view style="width: 100%; height: 50rpx; background-color: #6cb0f9;">1</view>
		<image src="../../static/tabbar3.jpg" mode="" style="width: 100%; height: 1150px; object-fit: cover;"></image>
		<u-tabbar v-model="current" active-color="#8dc9ff" icon-size="60" height="110" :list="list" :mid-button="true"></u-tabbar>
	</view>
</template>

<script>
	import {tabbar} from "@/util/common.js";
	export default {
		data() {
			return {
				list:tabbar,
				current: 0
			};
		}
	}
</script>

<style lang="scss">

</style>
