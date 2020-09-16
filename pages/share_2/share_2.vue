<template>
	<view>
		<view class="padding-lr-sm margin-lr-sm padding-top-sm padding-bottom-xl solid-bottom">
			<view class="flex">
				<image src="../../static/logo.png" mode="aspectFill" class="margin-right-sm" style="width: 200upx;height: 220upx;border-radius: 15upx;"></image>
				<view class="padding-right-sm flex flex-direction justify-between padding-top-sm padding-bottom-xl">
					<view class="text-black text-bold">理解孩子的需求，他们需要的是一门兴趣</view>
					<view class="text-black text-bold">第一节：线下交流会</view>
				</view>
			</view>
		</view>
		<view class="flex align-center justify-center flex-direction margin-lr-sm solid-bottom padding-tb-xl">
			<view class="text-green padding-bottom-sm">打卡成功</view>
			<image src="../../static/logo.png" mode="aspectFill"
			style="width: 240rpx;height: 300rpx;border-radius: 15rpx;"></image>
		</view>
		<view class="padding-tb-xl flex align-center justify-center flex-direction">
			<view style="position: relative;">
				<image src="../../static/flower.png" mode="aspectFill"
				style="width: 150rpx;height: 150rpx;"></image>
				<view class="bg-red-light text-red round" style="position: absolute;right: -70rpx;top: 50rpx;width: 60rpx;height: 60rpx;line-height: 65rpx;text-align: center;">
					×60
				</view>
			</view>
			<view class="text-red padding-top-sm">
				奖励60朵
			</view>
			<view class="text-red text-lg padding-top-lg">
				我的小伙伴小红花比我多
			</view>
		</view>
		<view class="margin bg-gray radius padding-lr padding-tb-xl" style="position: relative;">
			<view class="bg-white padding-lr-xs" style="position: absolute;top: -30rpx;left: 20rpx;">
				<image src="../../static/mark.png" mode="aspectFit"
				style="width: 60rpx;height: 60rpx;"></image>
			</view>
			<view class="text-center padding-bottom-xl solids-bottom">
				感谢LVRIGHT奖励的小红花
			</view>
		</view>
		<view class="padding-tb-xl">
			<view class="cu-bar"></view>
		</view>
		<view class=" padding-tb-xl btn-group cu-bar " style="position: fixed;bottom: 0;width: 100%;">
			<button class="cu-btn bg-gradual-blue round lg" style="font-size: 26rpx;">帮TA收集更多小红花</button>
			<button class="cu-btn bg-gradual-orange round lg" style="font-size: 26rpx;">购买课程</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				star:-1,//点击的花数量
			}
		},
		methods: {
			selectF(index){
				this.star = index
			}
		}
	}
</script>

<style>
	.un-select-f{
		opacity: .5;
	}
	.bg-red{
		background-color: #f43d45;
		color: #FFFFFF;
	}
	
	.bg-red-light{
		background-color: #fde0e4;
	}
	
	.text-red{
		color: #f43d45;
	}
	
	.bg-gray{
		background-color: #f7f7f7;
	}
	
	.line-red{
		color: #f43d45;
	}
	
	.line-red::after{
	  border-color: #f43d45;
	}

</style>
