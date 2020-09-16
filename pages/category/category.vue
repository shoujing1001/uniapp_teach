<template>
	<view >
		<!-- 左侧分类tab -->
		<view class="this-bg-gray"
		 style="width: 150upx;float: left; overflow-y:auto;overflow-x: hidden;height: 100%;position: fixed;">
			<view v-for="(e,index) in 10" :key="index" @click="selectTab(index)"
			:class="[sIndex == index ? 'bg-white' :'text-gray']" class="padding">分类{{index}}</view>
		</view>
		<!-- 右侧内容区域 -->
		<view  style="width: 600upx;height: 100%;float: right;">
			<view class="flex justify-between padding-sm align-center">
				<view class="text-black">共找到{{sIndex}}个课程</view>
				<view @click="showPop" class="line-orange cu-tag round" >
					<text class="text-black margin-left-xs">{{title}} <text class="icon-triangledownfill margin-left-xs"></text></text></view>
			</view>
			<view v-for="(item,index) in courseList" :key="index" class="margin-sm padding-sm"
			 style="border-radius: 15upx;background-color: #f9f9f9;width: 560upx;">
				<view class="flex">
					<view style="position: relative;">
						<image src="../../static/logo.png" mode="aspectFill" class="margin-right-sm"
						style="width: 180upx;height: 200upx;border-radius: 15upx;">
						</image>
						<view v-if="item == 'a' || item == 'b'" class="bg-cyan padding-xs text-sm"
						 style="position: absolute;top: 0;right: 20upx;border-top-right-radius: 15upx;border-bottom-left-radius: 15upx;">公益</view>
					</view>
					<view class="padding-right-sm flex flex-direction justify-between padding-tb-xs"
					style="width:340upx ;">
						<view class="text-lg text-bold text-black">理解孩子的需求</view>
						<view class="text-black text-cut" >80%的家长都不理解孩子的思维</view>
						<view class="text-grey text-cut">
							王教授 | 师范大学幼儿教育讲师
						</view>
						<view class="flex justify-between align-center">
							<view class="">
								<text class="text-red text-lg">￥99.00</text>
								<text class="margin-left-sm">21 章节</text>
							</view>
						</view>
					</view>
				</view>
				<view class="flex align-center" style="padding-left: 200upx;">
					<view class="text-cut text-gray"><text>2398</text>人正在参与</view>
					<view class="cu-avatar-group" style="flex-shrink: 0;">
						<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view>
						<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81005.jpg);"></view>
					</view>
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
	import chunLeiPopups from "@/components/chunLei-popups/chunLei-popups.vue"
	export default {
		data() {
			return {
				sIndex:0,
				//气泡菜单所需参数start
				list: [
					{title:'热门',id:1},{title:'最多人学',id:2},{title:'最新发布',id:3},{title:'免费课程',id:4},
					{title:'课程费用 从高到低',id:5},{title:'课程费用 从低到高',id:6},{title:'公益课程',id:7}
				],//气泡菜单列表，元素属性必须含有title，其他id属性可以自由定义，在回调中整个元素都会返回
				popx:344,//气泡x坐标，可从点击事件中获取
				popy:20,//气泡y坐标
				isShowPop:false,//控制是否显示
				//气泡菜单所需参数end
				courseList:['a','b','c','d','e','f','g'],//模拟课程列表
				title:'热门'
			}
		},
		onLoad() {
			//获取数据
			//this.getData()
		},
		onReachBottom() {
			this.getData()
		},
		components: { chunLeiPopups },
		methods: {
			selectTab(index){
				this.sIndex = index
				//滚动页面到顶部
				uni.pageScrollTo({
				    scrollTop: 0,
				    duration: 300
				});
				//根据分类重新获取数据
				//this.getData()
				//模拟重载
				const that = this
				uni.showLoading({
					title:"获取数据中..."
				})
				//接口获取数据，回调中处理
				setTimeout(function() {
					that.courseList = ['a','b','c','d','e','f','g'];
					uni.hideLoading();
				}, 1000*2);
			},
			tapPopup(e){
				console.log(e)
				this.title = e.title
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
					that.courseList = that.courseList.concat(that.courseList);
					uni.hideLoading();
				}, 1000*2);
			}
		}
	}
</script>

<style>
	.this-bg-gray{
		background-color: #f9f9f9;
	}
	
	.bg-cyan{
		background-color: #15d396;
	}
	
</style>
