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
			<map style="width: 95%; height: 350px;"
			 :latitude="latitude" :longitude="longitude" :markers="markers"
			 :show-location="true" id="map1">
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
		<!-- 自定义弹窗 -->
		<uni-popup ref="popup" type="center" :custom="true">
			<view class="bg-white " style="padding-top: 30rpx;padding-bottom: 30rpx;width: 670rpx;border-radius: 15rpx;">
				<view class="text-center">第一关：数灯笼</view>
				<view class="padding-tb-sm text-center text-lg text-black">数数这里到底有多少灯笼呢？</view>
				<view class="flex justify-center">
					<image src="../../static/logo.png" mode="aspectFill"
					 style="border-radius: 15upx;height: 300upx;width: 90%;"
					 ></image>
				</view>
				<view v-if="ansType == '输入'" class="solid-bottom padding-tb-sm text-center">
					<input placeholder="请输入你的答案" class="text-df text-center" />
				</view>
				<view v-if="ansType == '选择题'" class="cu-bar btn-group padding-tb-sm">
					<button @click="selectAns(0)" :class="[ansIndex == 0 ?'bg-gradual-orange':'bg-gray']" class="cu-btn round lg">4个</button>
					<button @click="selectAns(1)" :class="[ansIndex == 1 ?'bg-gradual-orange':'bg-gray']" class="cu-btn round lg">5个</button>
					<button @click="selectAns(2)" :class="[ansIndex == 2 ?'bg-gradual-orange':'bg-gray']" class="cu-btn round lg">6个</button>
				</view>
				<view v-if="ansIndex == 0" class="text-center text-red">答案错误啦！</view>
				<view class="cu-bar btn-group padding-lr-sm padding-tb">
					<button @click="cancel" class="bg-gradual-gray cu-btn round lg">取消</button>
					<button @click="submit" class="bg-gradual-orange cu-btn round lg" style="width: 188rpx;">提交</button>
				</view>
			</view>
		</uni-popup>
		<!-- 打卡提醒 -->
		<uni-popup ref="popup1" type="center" :custom="true">
			<view class="bg-white " style="padding-top: 30rpx;padding-bottom: 30rpx;width: 670rpx;border-radius: 15rpx;">
				<view v-if="clockType=='打卡'" class="flex justify-center align-center flex-direction">
					<image src="../../static/appicon.png" mode="aspectFill"
					style="width: 100upx;height: 100upx;"></image>
					<view class="text-lg text-black padding-tb-sm">恭喜你，打卡成功啦~</view>
					<button @click="clockSucc" class="cu-btn bg-gradual-orange round lg">好的</button>
				</view>
				<view v-if="clockType=='完成'" class="flex justify-center align-center flex-direction">
					<image src="../../static/appicon.png" mode="aspectFill"
					style="width: 100upx;height: 100upx;"></image>
					<view class="text-lg text-black padding-tb-sm">你已完成本课程啦</view>
					<button @click="clockSucc" class="cu-btn bg-gradual-orange round lg">好的</button>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from "@/components/uni-popup/uni-popup.vue"
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
				ansIndex:99,//选项答案
				ansType:"输入",
				over:false,
				clockType:'完成'
			}
		},
		//实时定位，兼容h5和app端只有重复调用uni接口
		onLoad() {
			this.getCurrentLocation();
		},
		components: {uniPopup},
		methods: {
			setMyLocation(latitude,longitude){
				this.markers[0].latitude = latitude;
				this.markers[0].longitude = longitude;
				var map = uni.createMapContext('map1');
				map.translateMarker({
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
				this.$refs.popup.open()
			},
			selectAns(index){
				this.ansIndex = index;
			},
			cancel(){
				//关闭弹窗
				this.$refs.popup.close()
			},
			submit(){
				//提交签到
				this.$refs.popup.close()
				this.over = true,
				this.$refs.popup1.open()
			},
			//打卡成功后关闭提醒
			clockSucc(){
				this.$refs.popup1.close();
			}
		}
	}
</script>

<style>

</style>
