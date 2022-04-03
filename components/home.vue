<template>
	<view>
		<u-tabbar v-model="current" :list="list" :mid-button="true" :before-switch="beforeSwitch"></u-tabbar>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				uCurrent:0,
				list: [ 
					{ 
						iconPath: "home",
						selectedIconPath: "home-fill",
						text: '首页',
						count: 2,
						isDot: true,
						customIcon: false,
						pagePath:'/pages/index/index'
					},
					{
						iconPath: "https://cdn.uviewui.com/uview/common/min_button.png",
						selectedIconPath: "https://cdn.uviewui.com/uview/common/min_button_select.png",
						text: '发布',
						midButton: true,
						customIcon: false,
					},
					{
						iconPath: "account",
						selectedIconPath: "account-fill",
						text: '我的',
						count: 23,
						isDot: false,
						customIcon: false,
						pagePath:'/pages/my/my'
					},
				],
				current: 0
			};
		},
		methods:{
			topSwiperTab(e){
				this.uCurrent =Number(e.target.current)
				// number(e.target.current)
				// console.log(this.uCurrent);
			},
			beforeSwitch(index) {
				console.log(index)
				// 返回一个promise
				
				uni.navigateTo({
					url:this.list[index].pagePath
				})
			}
		}
	}
</script>

<style lang="scss">
.slot-wrap{
		// background: url(../../static/navbar.png);
		width: 750rpx;
		display: flex;
		justify-content: space-between;
		padding-left: 20rpx;
		padding-right: 20rpx;
		.title{
			color: white;
			font-size: 32rpx;
			font-weight: bold;
		}
		.icon{
			width: 180rpx;
			display: flex;
			justify-content: space-between;
			font-weight: bold;
			color: white;
			.icon-sousuo{
				font-size: 41rpx !important;
			}
			.icon-qiandao{
				font-size: 41rpx !important;
			}
			.icon-saoma{
				font-size: 32rpx;
				margin-top: 6rpx;
			}
		}
		
	}
	.content{
		width: 750rpx;
		background: #f5f7f6;
		.swiper-bg{
			width: 100%;
			height: 400rpx;
			position: absolute;
			border-radius: 50rpx;
			top: -100rpx;
			padding-left: 20rpx;
			padding-right: 20rpx;
			background: linear-gradient(45deg, rgb(132, 0, 0), rgb(247, 118, 39),rgb(196, 4, 2));
			
		}
		.content-top{
			position: relative;
			top: 0rpx;
			
			padding-left: 20rpx;
			padding-right: 20rpx;
			swiper{
				width: 100%;
				height: 290rpx;
				border-radius: 20rpx;
				overflow: hidden;
				image{
					width: 100%;
					height: 100%;
				}
				background: #000;
			}
			.rect{
				position: relative;
				width: 100%;
				height: 50rpx;
				display: flex;
				justify-content: center;
				align-items: center;
				.u-indicator-item-rect{
					width: 15rpx;
					height: 15rpx;
					border-radius: 50%;
					background: white;
					margin-left: 20rpx;
					background: #eeb2b4;
				}
				.active{
					width: 30rpx;
					border-radius: 20rpx;
					background-color: red;
				}
			}
		}
		
		
		// height: 750rpx;
		// background: #000;
	}
</style>
