<template>
	<view>
		<u-navbar :is-back="false"   :background="background" :border-bottom="false" class="navbar">
			<view class="slot-wrap">
				<view class="title">
					广州科技贸易职业学院 · 易班
				</view>
				<view class="icon">
					<view class="sousuo"></view>
					<view class="qiandao"></view>
					<view class="saoma"></view>
				</view>
			</view>
		</u-navbar>
		<view class="content">
			<!-- 正文内容 -->
			<view class="swiper-bg">
			</view>
			<view class="content-top">
				<swiper @change="topSwiperTab" :current="uCurrent" circular  :autoplay="true" :interval="3000" :duration="1000">
					<swiper-item>
						<image src="../../static/banner1.jpg" mode=""></image>
					</swiper-item>
					<swiper-item>
						<image src="../../static/banner2.jpg" mode=""></image>
					</swiper-item>
					<swiper-item>
						<image src="../../static/banner3.jpg" mode=""></image>
					</swiper-item> 
					<swiper-item>
						<image src="../../static/banner4.jpg" mode=""></image>
					</swiper-item>
				</swiper>
				<view class="rect" >	
					<view :class="['u-indicator-item-rect',index == uCurrent + 1 ? 'active' : '']" v-for="index in 4"></view>	
				</view>
			</view>
			
			<view class="content-nav">
				<image src="../../static/navbar.png" mode=""></image>
				<view class="clickxbh" @click="xiaobenhua"></view>
			</view>
			
			<u-sticky :offset-top="navoffsetTop" bg-color="#f7f7f7">
				<view class="content-tab" >
					<view class="tabs" >
						<u-tabs 
						 name="cate_name"
						 count="cate_count"
						 :list="Tablist" 
						 :is-scroll="false" 
						 bar-width="88" 
						 active-color="#000"  
						 :bar-style="barStyle" 
						 :current="Tabcurrent" 
						 @change="change"
						 bar-height="5"
						 height="100"
						 ref="abc"></u-tabs>
					</view>
				</view>
			</u-sticky>
			
			<view class="school" v-if="Tabcurrent == 0">
				<image src="../../static/tab1.jpg" mode=""></image>
			</view>
			<view class="original" v-else-if="Tabcurrent == 1">
				<image src="../../static/tab2.jpg" mode=""></image>
			</view>
			<view class="headline" v-else-if="Tabcurrent == 2">
				<image src="../../static/tab3.jpg" mode=""></image>
			</view>
			<view class="topPost" v-else-if="Tabcurrent == 3">
				<image src="../../static/tab4.jpg" mode=""></image>
			</view>
		</view>
		<u-tabbar v-model="TabbarCurrent" active-color="#8dc9ff" icon-size="60" height="110" :list="Tabbarlist" :mid-button="true"></u-tabbar>
	</view>
</template>

<script>
	import {tabbar,indexTabs} from "@/util/common.js";
	export default {
		onReady(){
				let tabsHeight = 0;
				let navHeight = 0;
				let tabTop = 0;
				let contentTopHeight = 0;
				let contentNavHeight = 0;
				const query = uni.createSelectorQuery().in(this);
				let that = this;
				query.select('.tabs').boundingClientRect(data => {
				  tabsHeight = data.height;
				  tabTop = data.top;
				})
				query.select('.content-top').boundingClientRect(data => {
				  // console.log("得到布局位置信息" + JSON.stringify(data));
				  contentTopHeight = data.height;
				})
				query.select('.content-nav').boundingClientRect(data => {
				  // console.log("得到布局位置信息" + JSON.stringify(data));
				  contentNavHeight = data.height;
				})
				query.select('.navbar').boundingClientRect(data => {
				  // console.log("得到布局位置信息" + JSON.stringify(data));
				  navHeight = data.height
				  that.navoffsetTop = (tabTop  -  contentTopHeight - contentNavHeight + navHeight) - 20
				  console.log(tabsHeight)
				}).exec();
				
				// console.log(that.navoffsetTop)
		},
		onReachBottom(e){
			
		},
		onPageScroll : function(e) { //nvue暂不支持滚动监听，可用bindingx代替
			if(e.scrollTop == 335){
				console.log("1")
			}
			if(parseInt(e.scrollTop) >= 155){
				this.background.backgroundColor = "#6db0f7"
			}else{
				this.background.backgroundColor = "rgba(0,0,0,0)"
			}
			
		},
		data() {
			return {
				uCurrent:0,
				Tabbarlist: tabbar,
				TabbarCurrent: 0,
				navoffsetTop : 0,
				background: {
					backgroundColor: 'rgba(0,0,0,0)',
					transition: "background-color 2s",
				},
				Tablist: indexTabs,
				Tabcurrent: 0,
				barStyle:{
					backgroundColor: '#6db0f7',
				},
			};
		},
		methods:{
			topSwiperTab(e){
				this.uCurrent =Number(e.target.current)
			},
			xiaobenhua(){
				uni.navigateTo({
				    url: '/pages/xiaobenhua/xiaobenhua'
				})
			},
			change(index){
				this.Tabcurrent = index;
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
		
		.title{
			color: white;
			font-size: 32rpx;
			font-weight: bold;
		}
	.icon{
		width: 180rpx;
		display: flex;
		justify-content: space-between;
		color: white;
		.sousuo{
			width: 40rpx;
			height: 40rpx;
			background-image: url(../../static/sousuo.png);
			background-size: cover;
		}
		.qiandao{
			width: 40rpx;
			height: 40rpx;
			background-image: url(../../static/qiandao.png);
			background-size: cover;
		}
		.saoma{
			width: 48rpx;
			height: 40rpx;
			background-image: url(../../static/erweima.png);
			background-size: cover;
		}
	}
		
}
.content{
	width: 750rpx;
	background: #f5f7f6;
	.swiper-bg{
		width: 100%;
		height: 600rpx;
		position: absolute;
		top: -100rpx;
		padding-left: 20rpx;
		padding-right: 20rpx;
		// background: linear-gradient(45deg, rgb(132, 0, 0), rgb(247, 118, 39),rgb(196, 4, 2));
		background: linear-gradient(180deg, rgb(109, 176, 247), rgb(109, 176, 247),rgb(255, 255, 255));
		border-bottom-right-radius: 20rpx;
		border-bottom-left-radius: 20rpx;
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
				background: #b2d7f2;
			}
			.active{
				width: 30rpx;
				border-radius: 20rpx;
				background-color: #67b2f2;
			}
		}
	}
	
	.content-nav{
		width: 100%;
		padding-left: 20rpx;
		padding-right: 20rpx;
		// margin-top: 10rpx;
		position: relative;
		image{
			width: 100%;
			height: 520rpx;
			object-fit: cover;
			border-radius: 20rpx;
			overflow: hidden;
			// position: relative;
		}
		.clickxbh{
			width: 100rpx;
			height: 100rpx;
			// background: #000;
			position: absolute;
			right: 188rpx;
			top: 50rpx;
		}
	}
	.content-tab{
		width: 100%;
		// 
		.tabs{
			 padding: 0 20rpx 0 20rpx;
			 // background: #000;
			.u-tabs{
				width: 100%;
				border-top-right-radius: 20rpx;
				border-top-left-radius: 20rpx;
				overflow: hidden;
			}
		}
		
	}
	.school{
		width: 100%;
		image{
			width: 100%;
			height: 1000px;
		}
	}
	.original,.headline,.topPost{
		width: 100%;
		image{
			width: 100%;
			height: 700px;
		}
	}
}
</style>
