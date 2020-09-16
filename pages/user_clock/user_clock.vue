<template>
	<view>
		<view class="padding-sm solid-bottom">
			<view class="flex">
				<image src="../../static/logo.png" mode="aspectFill" class="margin-right-sm" style="width: 200upx;height: 220upx;border-radius: 15upx;"></image>
				<view class="padding-right-sm flex flex-direction justify-between padding-tb-sm">
					<view class="text-black text-bold">理解孩子的需求，他们需要的是一门兴趣</view>
					<view class="text-grey">1/21章节 <text class="margin-left text-black">12分</text></view>
					<view class="text-black text-bold">第一节：松湖烟雨出发点</view>
				</view>
			</view>
		</view>
		<view class="margin-tb padding-lr-sm flex justify-center align-center flex-direction">
			<view class="text-gray">当前定位</view>
			<view class="text-black padding-top-sm">{{currentLocationName}}</view>
		</view>
		<view class="flex justify-center" style="border-radius: 15upx;">
			<map style="width: 710rpx; height: 350px;border-radius: 8px;"
			 :latitude="latitude" :longitude="longitude" :markers="markers" 
			 :show-location="true" @controltap="getLocation" id="map1">
			 <cover-image style="width: 80rpx;height: 80rpx;position: absolute;right: 40rpx;bottom: 60rpx;" @click="getLocation" src="../../static/location.png"></cover-image>
			</map>
			
		</view>
		<view class="cu-bar"></view>
		<view :class="over?'':'solid-top'" class="bg-white padding-tb-xs flex align-center justify-center flex-direction" style="position: fixed;bottom: 0;width: 100%;">
			<button v-if="!over" @click="clock" class="cu-btn bg-gradual-orange round lg" style="width: 80%;">签到</button>
			<view v-if="over" class="text-orange text-center">
				<view class="text-lg text-bold">用时00:04:13</view>
				<view class="">您已完成本次打卡</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				//地图中心位置
				latitude: 27.226848266072572,
				longitude: 107.8921982116699,
				currentLocationName:'正在获取定位中...',
				//地图标记
				markers: [{
					id:'maker1',//建议设为Number
					latitude: 27.226848266072572,
					longitude: 107.8921982116699,
					iconPath: '../../static/mapMakers/myLocation.png',
					width:50,
					height:50,
					label:{
						content:'我的位置',
						padding:10
					}
				},
				{
					id:'maker2',//建议设为Number
					latitude: 27.326848266072572,
					longitude: 107.9921982116699,
					iconPath: '../../static/mapMakers/qidian.png',
					width:50,
					height:50,
					label:{
						content:'起点',
						padding:10
					}
				},
				{
					id:'maker3',//建议设为Number
					latitude: 27.426848266072572,
					longitude: 108,
					iconPath: '../../static/mapMakers/wancheng.png',
					width:50,
					height:50,
					label:{
						content:'已完成',
						padding:10
					}
				},
				{
					id:'maker4',//建议设为Number
					latitude: 27.526848266072572,
					longitude: 108.1,
					iconPath: '../../static/mapMakers/weiwancheng.png',
					width:50,
					height:50,
					label:{
						content:'第三节',
						padding:10
					}
				},
				{
					id:'maker5',//建议设为Number
					latitude: 27.626848266072572,
					longitude: 108.2,
					iconPath: '../../static/mapMakers/weiwancheng.png',
					width:50,
					height:50,
					label:{
						content:'第四节',
						padding:10
					}
				}],
				controls:[
					{
						id:'location',
						position:{
							top:280,
							left:320,
							width:40,
							height:40
						},
						iconPath:'../../static/location.png',
						clickable:true
					}
				],
				over:false,
			}
		},
		//实时定位，兼容h5和app端只有重复调用uni接口
		onLoad() {
			this.$Map = uni.createMapContext('map1');
			this.getCurrentLocation();
			const that = this
			uni.$on('clockSucc',function(){
				that.over = true
			})
		},
		methods: {
			setMyLocation(latitude,longitude){
				this.markers[0].latitude = latitude;
				this.markers[0].longitude = longitude;
				
				this.$Map.translateMarker({
					markerId:'maker1',
					destination:{
						latitude: this.markers[0].latitude,
						longitude: this.markers[0].longitude,
					}
					
				})
			},
			getCurrentLocation(){
				const that = this;
				setInterval(function(){
					uni.getLocation({
					    type: 'wgs84',
						geocode:true,//返回位置，仅app端支持，为了兼容可以调用高德开放平台的接口解析经纬度获得位置信息
					    success: function (res) {
					        console.log('当前位置的经度：' + res.longitude);
					        console.log('当前位置的纬度：' + res.latitude);
							//修正地图中心位置以及地图上当前我的位置 因为h5端和app端表现不一致，故需手动处理
							that.longitude = res.longitude;
							that.latitude = res.latitude;
							that.setMyLocation(res.latitude,res.longitude);
							console.log(JSON.stringify(res.address));
							//条件编译处理
							// #ifdef APP-PLUS
							that.currentLocationName = res.address.city+res.address.district+res.address.street+res.address.streetNum+'';
							// #endif
					    }
					});
				},1000*5);//每五秒获取一次地理位置信息
			},
			clock(){
				// this.hideMap(true);//关闭app端地图
				// this.$refs.popup.open()
				//跳转到新页面打卡
				uni.navigateTo({
					url:"../new_clock_page/new_clock_page"
				})
			},
			
			
			hideMap(isShow){
				//控制app端地图显示和隐藏，避免遮盖弹窗
				// #ifdef APP-PLUS
				// var map = uni.createMapContext('map1');
				// // plusMap = plus.maps.getMapById('map1');
				// console.log(JSON.stringify(map))
				var plusMap = this.$Map.$getAppMap();
				console.log(plusMap);
				// if(!isShow){//显示
				// 	plusMap.show()
				// }else{//隐藏
				// 	plusMap.hide()
				// }
				// #endif
			},
			getLocation(){
				// this.getCurrentLocation()
				this.$Map.moveToLocation()
			}
		}
	}
</script>

<style>

</style>
