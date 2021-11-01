<template>
	<view>
		<u-navbar :is-back="true" height="50" class="navbar" back-icon-color="#fff"   :background="background" :border-bottom="false">
			<view class="slot-wrap">
				<view class="title">
					请销假
				</view>
				<view class="icon">
					<view class="iconfont icon-guanbi"></view>
					<view class="iconfont icon-caozuo"></view>
				</view>
			</view>
		</u-navbar>
		<view class="content">
			
			<view class="causeStyle">
				<view class="iconfont icon-bitian" style="height: 65rpx; line-height: 65rpx; font-size: 27rpx;">外出原因说明</view>
				<textarea @blur="getTextarea" maxlength='9999'/>
				<view style="display: flex; justify-content: space-between;">
					<view class="iconfont icon-bitian" style="height: 100rpx; line-height: 100rpx; font-size: 27rpx;">外出期间是否有课</view>
					
					<!-- <view :style=" {'height': '100rpx' ,'line-height': '100rpx','font-size': '27rpx',color: sValueColor || '#C0C0C0'  }"  @click="showSelector">{{sValue || "请选择"}}<u-icon name="arrow-right" color="#ccc"></u-icon></view> -->
					<view :style=" {'height': '100rpx' ,'line-height': '100rpx','font-size': '27rpx',color: sValueColor || '#C0C0C0'  }"  @click="showSelector">{{affairForm.sValue || "请选择"}}<u-icon name="arrow-right" color="#ccc"></u-icon></view>
					<u-picker mode="selector" v-model="show" :range="selector",  :default-selector="[0]" @confirm="selectorValue"></u-picker>
				</view>
			</view>
			<view class="content-middle">
				<view class="materials">
					<view class="">请假条及其他相关作证材料</view>
					<view class="">最多上传9张，大小10M以内</view>
				</view>
				<!-- <u-upload ref="uUpload" :on-error="getImage" :auto-upload="false" ></u-upload> -->
				<!-- <button type="default" @click="getImage">上传图片</button> -->
				<view style="display: flex; padding-left: 20rpx;">
					<image v-if="fileImage.length !== 0" v-for="(item,index) in fileImage" :src="item" style="width: 200rpx; height: 200rpx; margin-right: 10rpx; flex-wrap: inherit;" mode=""></image>
					<view class="uploadImage"  @click="getImage">+</view>
				</view>
				<view class="affair">
					
					<u-form :model="affairForm" ref="uForm">
							<view style="display: flex; align-items: center;">
								<view class="iconfont icon-bitian"></view>
								<u-form-item label-width="200" label="开始时间"><u-input v-model="affairForm.startTime" placeholder="请输入开始时间 格式为: 00:00"/></u-form-item>
							</view>
							<view style="display: flex; align-items: center;">
								<view class="iconfont icon-bitian"></view>
								<u-form-item label-width="200" label="结束时间"><u-input v-model="affairForm.endTime" placeholder="请输入结束时间 格式为: 23:59"/></u-form-item>
							</view>
							<view style="display: flex; align-items: center;">
								<view class="iconfont icon-bitian"></view>
								<u-form-item label-width="200" label="时长(天)"><view class="">{{setTime}}</view></u-form-item>
							</view>
							<view style="display: flex; align-items: center;">
								<view class="iconfont icon-bitian"></view>
								<u-form-item label-width="200" label="请假类型" ><u-input placeholder="请输入请假类型: 事假/病假/其他" v-model="affairForm.leave" /></u-form-item>
							</view>
					</u-form>
				</view>
			</view>
			<view class="content-affair">
				<u-form :model="relationForm" ref="uForm">
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="名字"><u-input placeholder="请输入你的名字" v-model="relationForm.userName" /></u-form-item>
						</view>
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="性别"><u-input placeholder="请输入你的性别" v-model="relationForm.sex" /></u-form-item>
						</view>
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="本人联系电话"><u-input placeholder="请输入本人联系电话" v-model="relationForm.phone" /></u-form-item>
						</view>
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="学号"><u-input placeholder="请输入你的学号" v-model="relationForm.StudentID" /></u-form-item>
						</view>
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="紧急联系人"><u-input placeholder="请输入紧急联系人姓名" v-model="relationForm.urgency" /></u-form-item>
						</view>
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="紧急联系电话"><u-input placeholder="请输入紧急联系人电话" v-model="relationForm.urgencyPhone" /></u-form-item>
						</view>
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="交通方式" ><u-input placeholder="请输入交通方式: 公交/步行/地铁" v-model="relationForm.traffic" /></u-form-item>
						</view>
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="学院"><u-input placeholder="请输入你的学院" v-model="relationForm.college" /></u-form-item>
						</view>
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="专业"><u-input placeholder="请输入你的专业" v-model="relationForm.major" /></u-form-item>
						</view>
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="班级"><u-input placeholder="请输入你的班级" v-model="relationForm.class" /></u-form-item>
						</view>
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="年级"><u-input placeholder="请输入你的年级 例如2020" v-model="relationForm.grade" /></u-form-item>
						</view>
						
				</u-form>
				
			</view>
			<u-notice-bar mode="horizontal"  :duration="1000" :list="list"></u-notice-bar>
			<view class="content-personage">
				<u-button class="u-button"  :custom-style="customStyle" @click="addApprover">添加审批人</u-button>
				<view>
					<u-form :model="classForm" ref="uForm">
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="审批人"><u-input placeholder="请输入审批人名字" v-model="classForm.teacherName" /></u-form-item>
						</view>
						<view style="display: flex; align-items: center;">
							<view class="iconfont icon-bitian"></view>
							<u-form-item label-width="200" label="审批人编号" ><u-input placeholder="请输入审批人编号" v-model="classForm.teacherID" /></u-form-item>
						</view>
						
						<view class="" v-for="item in classFormList">
							<view style="display: flex; align-items: center;">
								<view class="iconfont icon-bitian"></view>
								<u-form-item label-width="200" label="审批人"><u-input placeholder="请输入审批人名字" v-model="item.teacherName" :disabled="true" /></u-form-item>
							</view>
							<view style="display: flex; align-items: center;">
								<view class="iconfont icon-bitian"></view>
								<u-form-item label-width="200" label="审批人编号" ><u-input placeholder="请输入审批人编号" v-model="item.teacherID" :disabled="true" /></u-form-item>
							</view>
						</view>
					</u-form>
				</view>
			</view>
			<u-top-tips ref="uTips" :navbar-height="80"></u-top-tips>
			<u-button class="u-button"  :custom-style="customStyle" @click="getMassage">提交</u-button>
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
					backgroundColor: '#51aefe',
				},
				// textareaValue: '',
				height: 260,
				show:false,
				selector: ["是","否"],
				sValue: '',
				sValueColor: '',
				fileList: [],
				action: 'http://www.example.com/upload',
				// startTimeValue: '',
				affairForm: {
					startTime: '',
					endTime: '',
					duration: '',
					leave: '',
					sValue:'',
					textareaValue:'',
					image: '',
					date:''
				},
				relationForm: {
					phone: '',
					userName:'',
					StudentID: '',
					urgency: '',
					urgencyPhone: '',
					traffic: '',
					class: '',
					college:'',
					major:'',
					grade:'',
					sex:''
				},
				classForm:{
					teacherName: '',
					teacherID: ''
				},
				list:[
					"辅导员和班主任编号是审批进度下面跟着名字的那串数字"
				],
				leaveList: [],
				fileImage:[],
				classFormList:[]
			};
		},
		onShow(){
			
			try {
				this.leaveList = JSON.parse(uni.getStorageSync("storage_leaveList"));
				this.relationForm = JSON.parse(uni.getStorageSync("storage_relationForm"));
			} catch (e) {
			    // error
			}
		},
		computed:{
			setTime(){
				let startTime = this.affairForm.startTime.replace(':','.') / 24
				let endTime = this.affairForm.endTime.replace(':','.') / 24
				this.affairForm.duration = Math.round((endTime - startTime)*100)/100
				if(this.affairForm.duration == 0)return "时长自动计算"
				return this.affairForm.duration
			}
		},
		methods:{
			addApprover(){
				this.classFormList.push(this.classForm)
				this.classForm = {}
				console.log(this.classFormList)
			},
			showSelector(){
				this.show = true
			},
			selectorValue(e){
				this.affairForm.sValue = this.selector[e]
				this.sValueColor = '#444444'
			},
			getTextarea(e){
				this.affairForm.textareaValue = e.target.value;
			},
			getMassage(){
				if(this.classForm.instructorID == ''){
					this.classForm.instructorID = '2016350011'
				}
				if(this.classForm.teacherID == ''){
					this.classForm.teacherID = '2016350011'
				}
				
				let startTime = this.affairForm.startTime.replace(':','.')
				let endTime = this.affairForm.endTime.replace(':','.')
				
				if(startTime < 0 || startTime.startsWith('-')){
					this.$refs.uTips.show({
						title: '时间异常，自动修正',
						type: 'error',
						duration: '3000',
					})
					this.affairForm.startTime = '00:00'
				}
				if(endTime > 23.59 || endTime.startsWith('-')){
					this.$refs.uTips.show({
						title: '时间异常，自动修正',
						type: 'error',
						duration: '3000',
					})
					this.affairForm.endTime = '23:59'
				}
				this.affairForm.date = this.$u.timeFormat(new Date().getTime())
				this.leaveList.unshift({
					affairForm: this.affairForm,
					relationForm: this.relationForm,
					classForm: this.classFormList,
				})
			
				try {
				    uni.setStorageSync('storage_leaveList', JSON.stringify(this.leaveList));
				    uni.setStorageSync('storage_relationForm', JSON.stringify(this.relationForm));
				
					
				} catch (e) {
				    // error
				}
			},
			getImage(res, index, lists, name){
				// console.log(res, index, lists, name)
				const that = this
				uni.chooseImage({
				    count: 1, //默认94
				    sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
				    sourceType: ['album'], //从相册选择
				    success: function (res) {
				        // console.log(JSON.stringify(res.tempFilePaths[0]));
						console.log(res)
						// uni.setStorageSync('storage_image', res.tempFilePaths[0]);
						that.fileImage.push(res.tempFilePaths[0])
						that.affairForm.image = that.fileImage
				    }
				});
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
		height: 44px;
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
		width: 750rpx;
		height: 900px;
		background: #f5f7f6;
		.causeStyle{
			width: 750rpx;
			padding-left: 20rpx;
			padding-right: 20rpx;
			background-color: #fff;
			textarea{
				width: 100%;
				padding: 20rpx;
				border-bottom: 1rpx solid #ccc;
				height: 220rpx;
			}
		}
		.content-middle{
			width: 100%;
			background: #fff;
			margin-top: 20rpx;
			.materials{
				padding-left: 25rpx;
				padding-top: 20rpx;
				view{
					
					margin-bottom: 10rpx;
					&:nth-child(2){
						font-size: 23rpx;
						color: #7c7c7c;
					}
				}
			}
			.u-upload{
				margin-left: 17rpx;
			}
			.affair{
				padding-left: 20rpx;
				.u-input{
					width: 400rpx;
				}
			}
		}
		.content-affair,.content-personage>view{
			margin-top: 20rpx;
			width: 100%;
			background: #fff;
			padding-left: 25rpx;
			.u-input{
				width: 400rpx;
			}
		}
		.content-personage{
			.u-notice-bar{
				margin: 0;
				padding: 0;
			}
		}
	}
	
	.uploadImage{
		width: 200rpx;
		height: 200rpx;
		border: 1rpx solid #ccc;
		text-align: center;
		line-height: 200rpx;
		font-size: 88rpx;
		margin-left: 25rpx;
		color: #ccc;
	}
</style>
