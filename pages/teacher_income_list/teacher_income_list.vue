<template>
	<view>
		<view class="flex align-center justify-center flex-direction padding">
			<image src="../../static/appicon.png" mode="aspectFill" class="round margin-sm" style="width: 120upx;height: 120upx;"></image>
			<view class="text-gray padding-tb-xs">总收益</view>
			<view class="text-bold text-black text-xl padding-tb-xs">65485.00</view>
		</view>
		<view class="padding-tb solid-top flex justify-between padding-lr-sm">
			<view class="text-gray">收益明细</view>
			<view @click="showPop" class="text-black">筛选<text class="margin-left-xs icon-filter"></text></view>
		</view>
		<view v-for="(item,index) in incomeList" :key="index" class="padding-tb padding-lr-sm solid-bottom" style="line-height: 1.6;">
			<view class="text-black text-bold">lvright 购买 《理解孩子的需求》课程</view>
			<view class="flex justify-between">
				<view class="text-gray">2019-12-11 14:22</view>
				<view class="text-orange">+ <text class="text-bold  text-xl">56.00</text></view>
			</view>
		</view>
		<chunLei-popups :dynamic="true" :value="isShowPop" :popData="list" @tapPopup="tapPopup" 
		:x="popx" :y="popy" placement="top-end">
		</chunLei-popups>
	</view>
</template>

<script>
	import xflSelect from '../../components/xfl-select/xfl-select.vue';     //导入
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
				//气泡菜单所需参数end
				incomeList:['a','b','c','d','e','f','g']//模拟课程列表
			}
		},
		onLoad() {
			this.getData();
		},
		onReachBottom() {
			this.pageIndex ++;
			this.getData();
		},
		components: { xflSelect,chunLeiPopups },
		methods: {
			tapPopup(e){
				console.log(e)
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
					that.incomeList = that.incomeList.concat(that.incomeList);
					uni.hideLoading();
				}, 1000*2);
			}
		}
	}
</script>

<style>

</style>
