<script>
	import md5Libs from "uview-ui/libs/function/md5";
	export default {
		onLaunch: function() {
			uni.setStorageSync('encryption', md5Libs.md5('6c15a30fc44f0cb313168c5dcae1e9632184491e52d0a2934bd260874cdcc3f0'));
			if(uni.getStorageSync('isEncryption') === ''){
				uni.reLaunch({
					url: '/pages/encryption/encryption'
				});
			}
			try {
				if(JSON.parse(uni.getStorageSync("storage_leaveList")).length >= 5){
					uni.setStorageSync('storage_leaveList', JSON.stringify(JSON.parse(uni.getStorageSync("storage_leaveList")).slice(0,3)));
				}
			} catch (e) {
			    // error 
			}
			 
			
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	// 引入uView基础样式
	@import "uview-ui/index.scss";
	@import "./static/icon.css"
	
	/*每个页面公共css */
</style>
