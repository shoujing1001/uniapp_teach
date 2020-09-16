<template>
	<view>
		<view class="top-bg padding-tb flex justify-between">
			<image src="../../static/logo.png" class="margin-lr-sm " mode="aspectFill" style="width: 270upx;height: 270upx;border-radius: 15upx;"></image>
			<view class="padding-right-sm flex flex-direction justify-between">
				<view class="padding-tb text-xl text-bold text-black">理解孩子的需求，他们需要的是一门兴趣</view>
				<view class="padding-tb flex align-center">
					<view><text>2398</text>人在购买</view>
					<view class="cu-avatar-group">
						<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view>
						<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81005.jpg);"></view>
					</view>
				</view>
			</view>
		</view>
		<view class="padding-tb solid-bottom flex justify-between padding-lr-sm">
			<view class="text-gray">课程购买用户</view>
			<view @click="showPop" class="text-black">筛选<text class="margin-left-xs icon-filter"></text></view>
		</view>
		<!-- 购买用户列表 -->
		<view class="">
			<view v-for="(item,index) in userList" :key="index" class="margin-lr-sm solid-bottom padding-tb-sm flex align-center">
				<image src="../../static/logo.png" mode="aspectFill" class="round" style="width: 100rpx;height: 100rpx;"></image>
				<view class="padding-left">
					<view class="text-bold text-lg">王大锤 <text>17606698523</text></view>
					<view class="text-gray">购买时间：2019-12-11 14:22</view>
				</view>
			</view>
		</view>
		<chunLei-popups :dynamic="true" :value="isShowPop" :popData="list" @tapPopup="tapPopup"
		:x="popx" :y="popy" placement="top-end">
		</chunLei-popups>
	</view>
</template>

<script>
	//气泡菜单文档 https://ext.dcloud.net.cn/plugin?id=801
	import chunLeiPopups from "@/components/chunLei-popups/chunLei-popups.vue";
	export default {
		data() {
			return {
				//气泡菜单所需参数start
				list: [
					{title:'热门',id:1},{title:'最多人学',id:2},{title:'最新发布',id:3},{title:'免费课程',id:4},
					{title:'课程费用 从高到低',id:5},{title:'课程费用 从低到高',id:6},{title:'公益课程',id:7}
				],//气泡菜单列表，元素属性必须含有title，其他id属性可以自由定义，在回调中整个元素都会返回
				popx:344,//气泡x坐标，可从点击事件中获取
				popy:20,//气泡y坐标
				isShowPop:false,//控制是否显示
				//气泡菜单所需参数\\end
				userList:['a','b','c','d','e','f','g','h','i','j','k','l','m']//模拟购买用户列表
			}
		},
		onLoad() {
			this.getData();
		},
		onReachBottom() {
			this.pageIndex ++;
			this.getData();
		},
		components:{chunLeiPopups},
		methods: {
			tapPopup(e){
				console.log(e)
				if(e == false){
					this.isShowPop = false
				}
				this.isShowPop = false
			},
			showPop(e){
				console.log(e)
				this.popx = e.mp.detail.x;
				this.popy = e.mp.detail.y;
				this.isShowPop = true
			},
			getData(){
				const that = this
				uni.showLoading({
					title:"获取数据中..."
				})
				//接口获取数据，回调中处理
				setTimeout(function() {
					that.userList = that.userList.concat(that.userList);
					uni.hideLoading();
				}, 1000*2);
			}
		}
	}
</script>

<style>
	.top-bg {
		background-color: #fffae8;
	}
</style>
