<template>
	<view>
		<scroll-view scroll-x class="bg-white nav text-center solid-bottom">
			<view class="cu-item" :class="sIndex==0?'my-cur text-black text-bold':'text-gray'"  @tap="tabSelect(0)">
				未发布
			</view>
			<view class="cu-item" :class="sIndex==1?'my-cur text-black text-bold':'text-gray'"  @tap="tabSelect(1)">
				已发布
			</view>
		</scroll-view>
		<view class="margin-sm padding-sm" style="border-radius: 15upx;background-color: #f3f3f3;">
			<view class="flex">
				<image src="../../static/logo.png" mode="aspectFill" class="margin-right-sm" style="width: 200upx;height: 220upx;border-radius: 15upx;"></image>
				<view class="padding-right-sm flex flex-direction justify-between padding-tb-sm">
					<view class="text-xl text-bold text-black">理解孩子的需求</view>
					<view class="text-black">80%的家长都不理解孩子的思维</view>
					<view class="text-grey">创建时间：2019-06-03</view>
					<view class="flex justify-between align-center padding-sm">
						<view class="">
							<text class="text-red">￥99.00</text>
							<text class="margin-left-sm">21 章节</text>
						</view>
						
					</view>
				</view>
			</view>
		</view>
		<view v-for="(item,index) in courseList" :key="index" class="margin-sm padding-sm" style="border-radius: 15upx;background-color: #fafafa;">
			<view class="flex">
				<image src="../../static/logo.png" mode="aspectFill" class="margin-right-sm" style="width: 200upx;height: 220upx;border-radius: 15upx;"></image>
				<view class="padding-right-sm flex flex-direction justify-between padding-tb-sm">
					<view class="text-xl text-bold text-black">理解孩子的需求</view>
					<view class="text-black">80%的家长都不理解孩子的思维</view>
					<view class="text-grey">创建时间：2019-06-03</view>
					<view class="text-red text-bold">未发布</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sIndex:0,
				courseList:['a','b','c','d','e','f','g']//模拟课程列表
			}
		},
		onLoad(opt) {
			this.sIndex = 0;
			this.getData();
		},
		onReachBottom() {
			this.pageIndex ++;
			this.getData();
		},
		methods: {
			//顶部tab选择
			tabSelect(index){
				this.sIndex = index
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
	.my-cur{
		border-bottom: #feab00 solid 5upx;
	}

</style>
