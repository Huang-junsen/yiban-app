<template>
	<view style="position: relative;">
		<u-navbar :is-back="true" height="50" class="navbar" back-icon-color="#fff" :background="background" :border-bottom="false">
			<view class="slot-wrap">
				<view class="title">
					{{leaveList.relationForm.userName}}的请销假
				</view>
				<view class="icon">
					<view class="iconfont icon-guanbi"></view>
					<view class="iconfont icon-caozuo"></view>
				</view>
			</view>
		</u-navbar>
		<view class="content" >
			<!-- <image src="../../static/shenpi.png" style="width: 180rpx; height: 150rpx; position: fixed; top: 180rpx; right: 40rpx; object-fit: cover;" mode=""></image> -->
			<view class="turnContainer">
			    <div class="bg">
			        <image class="inner" src="../../static/xing.png" mode="">
			    </div>
			</view>
			<view class="" style="width: 100%; height: 88rpx; background-color: #fff; font-size: 35rpx; text-align: center; line-height: 88rpx;">{{leaveList.relationForm.userName}}的请销假</view>
			<view> 
				<view class="titleBorder">申请人</view>
				<view class="userInfo" :class="{active: active == true ? 'active' : ''}">
					<view class="itemInfo" :style="{'margin-top': active == true ? '25rpx' : 0}" :class="{active: active != true ? 'active' : ''}" @click="test">
						<view class="title"   >姓名</view>
						<view :style="{'margin-right': active === true ? '15rpx' :''}">{{leaveList.relationForm.userName}}</view>
						<view v-if="active !== true">({{leaveList.relationForm.StudentID}})</view>
						<view class="iconfont icon-dianhua" style="color: #6db0f7; font-size: 23rpx; width: 35rpx; height: 35rpx; border-radius: 50%; border: 4rpx solid #6db0f7; line-height: 35rpx;"></view>
						<u-icon style="position: absolute; right: 30rpx;" :name="active === true ? 'arrow-up' : 'arrow-down'"></u-icon>
					</view> 
					<view class="itemInfo">
						<view class="title">学号</view>
						<view class="">{{leaveList.relationForm.StudentID}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">性别</view>
						<view class="">{{leaveList.relationForm.sex}}</view>
					</view>
					<view  class="itemInfo">
						<view class="title">学院</view>
						<view class="">{{leaveList.relationForm.college}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">系</view>
						<view class=""></view>
					</view>
					<view class="itemInfo">
						<view class="title">专业</view>
						<view class="">{{leaveList.relationForm.major}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">专业方向</view>
						<view class=""></view>
					</view>
					<view class="itemInfo">
						<view class="title">班级</view>
						<view class="">{{leaveList.relationForm.class}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">年级</view>
						<view class="">{{leaveList.relationForm.grade}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">教育层次</view>
						<view class="">专科</view>
					</view>
					<view class="itemInfo">
						<view class="title">学制</view>
						<view class="">3.0</view>
					</view>
				</view>
				<view class="titleBorder">申请内容</view>
				<view class="apply">
					<view class="itemInfo">
						<view class="title">审批编号</view>
						<view class="">{{date}}142647990600</view>
					</view>
					<view class="itemInfo">
						<view class="title">请假类型</view>
						<view class="">{{leaveList.affairForm.leave}}</view>
					</view>
					<view class="itemInfo"> 
						<view class="title">外出原因说明</view>
						<view class="" style="width: 520rpx;">{{leaveList.affairForm.textareaValue}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">外出期间是否有课</view>
						<view class="">{{leaveList.affairForm.sValue === "是" ? "有课" : "无课"}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">请假条或实习证明</view>
						<view class="">
							<image v-for="(item,index) in leaveList.affairForm.image" style="width: 150rpx; height: 150rpx; margin-right: 20rpx;" :src="item" mode=""></image>
						</view>
					</view>
					<view class="itemInfo">
						<view class="title">开始时间</view>
						<view class="">{{leaveList.affairForm.date}} {{leaveList.affairForm.startTime}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">结束时间</view>
						<view class="">{{leaveList.affairForm.date}} {{leaveList.affairForm.endTime}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">时长(天)</view>
						<view class="">{{leaveList.affairForm.duration}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">本人联系电话</view>
						<view class="">{{leaveList.relationForm.phone}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">紧急联系人</view>
						<view class="">{{leaveList.relationForm.urgency}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">紧急联系电话</view>
						<view class="">{{leaveList.relationForm.urgencyPhone}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">交通方式</view>
						<view class="">{{leaveList.relationForm.traffic}}</view>
					</view>
					<view class="itemInfo">
						<view class="title">承诺</view>
						<view class="" style="width: 520rpx;">本人已认真阅读过《广州科技贸易职业学院疫情期间学生返校行为规范指南（第一版）》，并对指南的内容承诺全部遵守。</view>
					</view>
				</view>
				<view class="titleBorder">审批进度</view>
				<view class="audit">
					<u-time-line style="position: relative;">
							<u-time-line-item nodeTop="2" v-for="(item,index) in leaveList.classForm">
								<!-- 此处自定义了左边内容，用一个图标替代 -->
								<template v-slot:node>
									<view class="u-node" style="background: #87d068; color: #fff;">
										<!-- 此处为uView的icon组件 -->
										1
									</view>
								</template>
								<template v-slot:content>
									<view style="display: flex; justify-content: space-between; padding-right: 30rpx;">
										<view class="u-order-title">{{item.teacherName}}({{item.teacherID}})</view>
										<view class="u-order-time">{{leaveList.affairForm.date}} {{consent}}</view>
									</view>
									<view style="color: #87d068; margin: 20rpx 0 20rpx 0; font-size: 30rpx;">已同意</view>
									<view style="color: #87d068; margin-left: -30rpx; font-size: 25rpx;">通过</view>
								</template>
							</u-time-line-item>
							<view style="width: 50rpx; border-bottom: 1rpx solid #ccc; position: absolute; left: -25rpx; bottom: 0;"></view>
						</u-time-line>
				</view>
			</view>
		</view>
		<view style="width: 100%; height: 88rpx;"></view>
		 <button style="width: 100%; height: 88rpx; position: fixed; bottom: 0; left: 0; z-index: 9;  border-radius: 0; color: #6db0f7;">转发审批表单</button>
		 
	</view>
</template>

<script>
	export default {
		data() {
			return {
				background: {
					backgroundColor: '#6db0f7'
				},
				active: false,
				// image: uni.getStorageSync("storage_image")
				leaveList: []
			};
		},
		methods:{
			test(){
				this.active = !this.active
			}
		},
		onLoad(options) {
			try {
				this.leaveList = JSON.parse(options.listObj);
				this.date = this.leaveList.affairForm.date.replace(/-/g,"")
				this.consent = this.leaveList.affairForm.startTime.split(":")[0]+":"+this.leaveList.affairForm.startTime.split(":")[1].split('')[0]+5
				
			} catch (e) {
			    // error
			}
			console.log(JSON.parse(options.listObj))
		}
	}
</script>

<style lang="scss">
	@keyframes spin{
	        to{transform: rotate(1turn);}
	    }
	.slot-wrap{
		width: 750rpx;
		display: flex;
		justify-content: space-between;
		padding-left: 20rpx;
		padding-right: 20rpx;
		align-items: center;
		.title{
			color: white;
			font-size: 34rpx;
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
	.content{
		width: 100%;
		background: #f5f7f6;
		// height: 900px;
		position: relative;
		z-index: 1;
		.turnContainer{
			width: 180rpx;
			height: 150rpx;
			position: fixed;
			// padding: 20px;
			top: 180rpx;
			right: 40rpx;
			border-radius: 100%;
			// object-fit: cover;
			.bg{
				width: 100%;
				height: 100%;
				background: url(../../static/turnBg.png) center center;
				background-size: cover;
				.inner{
					height: 100%;
					width: 100%;
					animation: spin 10s infinite linear;
					transform-origin: 50% 39px;
					object-fit: cover;
				}
			}
		}
		// .box{
		//         border-radius: 100%;
		//         padding: 20px;
		//         width: 120px;
		//         height: 100px;
		//     }
		//     .box .bg{
		//         width: 100%;
		//         height: 100%;
		//         background: url("底图.png") center center;
		//         background-size: cover;
		//     }
		//     .box .bg .inner{
		//         height: 100%;
		//         width: 100%;
		//         animation: spin 10s infinite linear;
		//         transform-origin: 50% 50px;
		//     }
		.titleBorder{
			width: 100%;
			height: 25rpx;
			margin: 30rpx 0 30rpx 20rpx; 
			padding-left: 10rpx; 
			border-left: 10rpx solid #6db0f7; 
			line-height: 25rpx;
		}
		.userInfo{
				width: 100%;
				height: 100rpx;
				background: #fff;
				// overflow: hidden;
				overflow: hidden;
				transition: all 0.5s;
				&.active{
					height: 750rpx;
				}
				.itemInfo{
					width: 100%; 
					font-size: 30rpx; 
					padding-left: 40rpx;
					display: flex;
					align-items: center;
					position: relative;
					font-size: 30rpx;
					box-sizing: border-box;
					margin-top: 25rpx; 
					// &:nth-child(1){
					// 	margin-top:0;
					// }
					&.active{
						height: 100rpx;
						line-height: 100rpx;
					}
					view{
						&:nth-child(2){
							margin-left: 20rpx;
						}
						&:nth-child(4){
							margin-left: 15rpx;
						}
					}
					.title{
						width: 150rpx;
						// background: #000;
						text-align: right;
						color: #a5a5a5;
					}
				}
			}
		.apply{
			width: 100%;
			background: #fff;
			padding-bottom: 40rpx;
			box-sizing: border-box;
			overflow: hidden;
			.itemInfo{
				width: 100%; 
				margin-top: 25rpx;
				font-size: 30rpx; 
				padding-left: 40rpx;
				display: flex;
				align-items: center;
				position: relative;
				font-size: 30rpx;
				box-sizing: border-box;
				view{
					&:nth-child(2){
						margin-left: 20rpx;
					}
					&:nth-child(4){
						margin-left: 15rpx;
					}
				}
				.title{
					width: 150rpx;
					// background: #000;
					text-align: right;
					color: #a5a5a5;
				}
			}
		}
		
		.audit{
			width: 100%;
			background: #fff;
			padding-bottom: 40rpx;
			overflow: hidden; 
			padding-left: 40rpx;
			padding-top: 40rpx; 
			box-sizing: border-box;
		}
			
	}
	
	
.img{
	width: 100%;
	height: 800px;
}

.u-node {
		width: 44rpx;
		height: 44rpx;
		border-radius: 100rpx;
		display: flex;
		justify-content: center;
		align-items: center;
		background: #d0d0d0;
	}
	
	.u-order-title {
		color: #333333;
		font-size: 30rpx;
	}
	
	.u-order-desc {
		color: rgb(150, 150, 150);
		font-size: 28rpx;
		margin-bottom: 6rpx;
	}
	
	.u-order-time {
		color: rgb(200, 200, 200);
		font-size: 26rpx;
	}
.u-time-axis::before{
	    border-left: 2px solid #87d068 !important;
}
</style>
