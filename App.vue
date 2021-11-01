<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
			// uni.clearStorageSync();
			try {
			    // console.log(JSON.parse(uni.getStorageSync("storage_leaveList")).length,"长度")
			    // console.log(JSON.parse(uni.getStorageSync("storage_leaveList")),"剩余")
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
