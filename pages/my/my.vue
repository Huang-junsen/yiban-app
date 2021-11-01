<template>
	<view>
		<view style="font-size: 38rpx; color: red;">仅供学习参考，任何违法行为与开发者无关，当你使用了本软件就代表你同意了这项规则!!!</view>
		<u-tabbar v-model="current" icon-size="60" active-color="#8dc9ff" height="110" :list="list" :mid-button="true"></u-tabbar>
	</view>
</template>

<script>
	import {tabbar} from "@/util/common.js";
	export default {
		data() {
			return {
				list: tabbar,
				current: 0
			}
		},
		methods: {
		}
	}
</script>

<style>
/* div{
	background: #8dc9ff;
} */
</style>
