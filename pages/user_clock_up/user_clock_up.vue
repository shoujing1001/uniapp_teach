<template>
	<view>
		<view class="padding-sm">
			<view class="flex">
				<image src="../../static/logo.png" mode="aspectFill" class="margin-right-sm" style="width: 200upx;height: 220upx;border-radius: 15upx;"></image>
				<view class="padding-right-sm flex flex-direction justify-between padding-tb-sm">
					<view class="text-black text-bold">理解孩子的需求，他们需要的是一门兴趣</view>
					<view class="flex align-center">
						<view><text>658</text>人已打卡</view>
						<view class="cu-avatar-group" style="flex-shrink: 0;">
							<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view>
							<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81005.jpg);"></view>
						</view>
					</view>
					<view class="text-black text-bold">第一节：线下交流会</view>
				</view>
			</view>
		</view>
		<view class="padding-tb margin-bottom margin-lr-sm solid-top flex justify-center align-center flex-direction">
			<view class="text-black ">拍摄打卡</view>
			<view class="text-sm padding-top-sm" :class="[upPic?'text-green':'text-gray']">
				{{upPic?'图片已上传，可以打卡了哦':'请先拍摄照片才能打卡哦'}}
			</view>
			<view class="flex justify-center padding-top-sm" style="width: 100%;">
				<view v-if="upPic == ''" @click="choosePic" class="flex align-center justify-center" style="width: 33.3%;height: 200upx;border: #999999 dashed 2upx;">
					<view class="icon-camera" style="font-size: 80upx;"></view>
				</view>
				<view v-if="upPic" @click="choosePic" class="flex align-center justify-center bg-img" 
				style="width: 33.3%;height: 200upx;"
				:style="'background-image:url('+upPic+')'"></view>
			</view>
			
		</view>
		
		<view class="padding-tb solid-top margin-lr-sm flex justify-center align-center flex-direction">
			<view class="text-black padding-top-sm">{{currentLocationName}}</view>
			<view class="text-gray">当前定位</view>
			<view class="margin-top-sm cu-btn round bg-gradual-blue lg">
				重新定位
			</view>
		</view>
		
		<view class="cu-bar"></view>
		<view class="solid-top bg-white padding-tb-xs flex align-center justify-center" style="position: fixed;bottom: 0;width: 100%;">
			<button class="cu-btn round lg" :class="[upPic?'bg-gradual-orange':'bg-gray']" style="width: 80%;">签到</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				latitude: 27.226848266072572,
				longitude: 107.8921982116699,
				currentLocationName:'正在获取定位中...',
				upPic:''
			}
		},
		onLoad() {
			this.getCurrentLocation();
		},
		methods: {
			getCurrentLocation(){
				const that = this;
				uni.getLocation({
				    type: 'wgs84',
					geocode:true,//返回位置，仅app端支持，为了兼容可以调用高德开放平台的接口解析经纬度获得位置信息
				    success: function (res) {
				        console.log('当前位置的经度：' + res.longitude);
				        console.log('当前位置的纬度：' + res.latitude);
						that.longitude = res.longitude;
						that.latitude = res.latitude;
						console.log(JSON.stringify(res.address));
						//条件编译处理
						// #ifdef APP-PLUS
						that.currentLocationName = res.address.city+res.address.district+res.address.street+res.address.streetNum+'';
						// #endif
				    }
				});
			},
			choosePic(){
				const that = this;
				uni.chooseImage({
				    count: 1, //默认9
				    sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
				    sourceType: ['album'], //从相册选择
				    success: function (res) {
				        console.log(JSON.stringify(res.tempFilePaths));
						that.upPic = res.tempFilePaths[0];
				    }
				});
			},
		}
	}
</script>

<style>
	.qidian{
		color: #00ca30;
	}
	
	.wancheng{
		color: #4978ff;
	}
	
	.disanjie{
		color: #ff4949;
	}

</style>
