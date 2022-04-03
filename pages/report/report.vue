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
			<!-- <askForleave></askForleave> -->
			<view class="leave">
				<!-- <view style="width: 750rpx; height: 43rpx; background-color: red;"></view> -->
				<view style="width: 750rpx; height: 43px;"></view>
				<view class="container-info" v-for="(item,index) in leaveList" @click="leave(item)">
					<view class="info-top">
						<view class="" style="font-size: 30rpx;">
							我的请假
						</view>
						<view  style="color: #9d9d9d; font-size: 25rpx;">
							{{item.affairForm.date}}
						</view>
					</view>
					<view class="info-middle">
						<view class="middle-top">
							<view class="middle-top-left" style="color: #929292;">
								<view>开始时间：{{item.affairForm.date}} {{item.affairForm.startTime}}:00</view>
								<view>结束时间：{{item.affairForm.date}} {{item.affairForm.endTime}}:59</view>
							</view>
							<view class="middle-top-right">
								<u-icon name="arrow-right" color="#929292" size="28"></u-icon>
							</view>
						</view>
						<view class="" style="color: #15a27f; margin-top: 30rpx; font-size: 30rpx;">
							审批通过
						</view>
						<view style="border-bottom: dashed  1px #ccc; margin-top: 20rpx;"></view>
						<view class="footer-title" v-if="index !== 0"> 
							<text class="font-weight">已于</text><text class="time" style="color: #05a1e7;">{{item.affairForm.date}} 23:59:59</text> <text class="font-weight">销假</text> <text class="iconfont icon-tupian" style="color: #93c8f3; font-size: 32rpx; font-weight: 500;"></text> 
						</view>
						<view class="footer-title" v-else>
							<text style="color: #05a1e7; font-size: 33rpx;">销假</text>
						</view>
					</view> 
				</view>
				<view class="container-info" v-for="index in 3">	
					<view class="info-top">
						<view class="" style="font-size: 30rpx;">
							我的请假
						</view>
						<view  style="color: #9d9d9d; font-size: 25rpx;">
							2021-7-11
						</view>
					</view>
					<view class="info-middle">
						<view class="middle-top">
							<view class="middle-top-left" style="color: #929292;">
								<view>开始时间：2021-10-14 21:55:00</view>
								<view>结束时间：2021-10-14 21:59:00</view>
							</view>
							<view class="middle-top-right">
								<u-icon name="arrow-right" color="#929292" size="28"></u-icon>
							</view>
						</view>
						<view class="" style="color: #15a27f; margin-top: 30rpx; font-size: 30rpx;">
							审批通过
						</view>
						<view style="border-bottom: dashed  1px #ccc; margin-top: 20rpx;"></view>
						<view class="footer-title"> 
							<text class="font-weight">已于</text><text class="time" style="color: #05a1e7;">2021-10-14 23:59:59</text> <text class="font-weight">销假</text> <text class="iconfont icon-tupian" style="color: #93c8f3; font-size: 32rpx; font-weight: 500;"></text> 
						</view>
					</view>
				</view>
				<view style="width: 750rpx; height: 88rpx; "></view>
			</view>
			<u-button class="u-button"  :custom-style="customStyle" @click="navigateClearLeave">请假申请</u-button>
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
				customStyle: {
					// marginTop: '20px', // 注意驼峰命名，并且值必须用引号包括，因为这是对象
					color: '#fff',
					backgroundColor: '#51aefe'
				},
				applyTop: 0,
				title:"学生外出报备",
				leaveList: [],
			};
		},
		created(){
			// var SevenDayAgo = timeStamp - 86400 * 9;
			// console.log(new Date().getTime() + (7 * 24 * 3600 * 1000))
			// console.log(timeStamp + (86400 * 7))
			// console.log(this.$u.timeFormat(timeStamp + (5 * 24 * 3600 * 1000), 'yyyy-mm-dd'))
			try {
				this.leaveList = JSON.parse(uni.getStorageSync("storage_leaveList"));
				console.log(this.leaveList,"创建");
			} catch (e) {
			    // error
			}
		},
		methods:{
			navigateClearLeave(){
				let that = this;
				uni.navigateTo({
					url:"/pages/clearLeave/clearLeave",
					events: {
						someEvent: function(response) {
							const {data} = response;
							that.leaveList = data; 
						}
					}
				})
			},
			leave(e){
				uni.navigateTo({
					url:"/pages/leave/leave?listObj=" + encodeURIComponent(JSON.stringify(e))
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

.leave{
		width: 100%;
		height: 100%;
		overflow: hidden;
		.container-info{
				width: 93%;
				height: 385rpx;
				background: white;
				margin: 25rpx auto;
				padding: 20rpx;
				.info-top{
					display: flex;
					justify-content: space-between;
					margin-top: 18rpx;
				}
				.info-middle{
					.middle-top{
						display: flex;
						justify-content: space-between;
						align-items: center;
						.middle-top-left{
							height: 100rpx;
							margin-top: 20rpx;
							display: flex;
							flex-direction: column;
							justify-content: center;
							justify-content: space-between;
						}
						.middle-top-right{
							margin-top: 25rpx;
						}
					}
					.footer-title{
						// margin: 0 auto;
						text-align: center;
						margin-top: 20rpx;
						.font-weight{
							font-weight: 600;
							font-size: 30rpx;
							margin-right: 10rpx;
							margin-left: 10rpx;
						}
						.time{
							font-weight: bold;
							font-size: 25rpx;
							margin-left: 5rpx;
							margin-right: 5rpx;
						}
					}
				}
			}
	}

</style>
