<template>
	<view class="encryption">
		<u-alert-tips type="warning" :title="title" :description="description"></u-alert-tips>
		<view class="Certification">
			<text>认证：</text><input type="text" v-model="encryption" placeholder="请输入认证码" />
		</view>
		<button type="default" @click="jumpPage">认证</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '使用须知',
				description: '点击认证后，使用者必须承担自身风险以及违法行为，仅供学习参考，任何违法行为与开发者无关，当你使用了本软件就表示你同意了这项规则',
				encryption: ''
			};
		},
		methods:{
			jumpPage(){
				const encryption = uni.getStorageSync('encryption');
				if(this.encryption === encryption){
					uni.reLaunch({
						url: '/pages/index/index'
					});
					uni.showToast({
					    title: '认证成功',
					    duration: 2000
					});
					uni.setStorageSync('isEncryption','true');
				}
			}
		}
	}
</script>

<style lang="scss">
	.encryption{
		.Certification{
			width: 100%;
			height: 30px;
			border: 1px solid #ccc;
			display: flex;
		}
	}

</style>
