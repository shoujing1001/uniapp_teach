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
			<view class="flex">
				<image v-for="index in 5" :key="index" @click="selectF(index)" 
				:class="[star >= index?'':'un-select-f']" 
				src="../../static/flower.png" mode="aspectFill" style="width: 65rpx;height: 65rpx;margin: 0 8rpx;"></image>
			</view>
			<view class="flex flex-wrap padding justify-center">
				<view :class="[tagIndex == 0?'bg-red':'bg-gray']" @click="selectT(0)" class="margin-right-xs margin-bottom-sm text-sm" style="line-height:2; padding: 0 25rpx;border-radius: 5000rpx;">
					真优秀
				</view>
				<view :class="[tagIndex == 1?'bg-red':'bg-gray']" @click="selectT(1)" class="margin-right-xs margin-bottom-sm text-sm" style="line-height: 2;padding: 0 25rpx;border-radius: 5000rpx;">
					孩子真聪明
				</view>
				<view  :class="[tagIndex == 2?'bg-red':'bg-gray']" @click="selectT(2)" class="margin-right-xs margin-bottom-sm text-sm" style="line-height: 2;padding: 0 25rpx;border-radius: 5000rpx;">
					值得鼓励
				</view>
				<view :class="[tagIndex == 3?'bg-red':'bg-gray']" @click="selectT(3)" class=" margin-right-xs margin-bottom-sm text-sm" style="line-height: 2;padding: 0 25rpx;border-radius: 5000rpx;">
					父母教导有方
				</view>
			</view>
			<button class="cu-btn round line-red">奖励TA</button>
		</view>
		<view class="margin bg-gray radius padding-lr padding-tb-xl" style="position: relative;">
			<view class="bg-white padding-lr-xs" style="position: absolute;top: -30rpx;left: 20rpx;">
				<image src="../../static/mark.png" mode="aspectFit"
				style="width: 60rpx;height: 60rpx;"></image>
			</view>
			<view class="padding-bottom-xl solids-bottom">
				<input placeholder="请输入" class="text-center text-df" />
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
				tagIndex:-1
			}
		},
		methods: {
			selectF(index){
				this.star = index
			},
			selectT(index){
				this.tagIndex = index
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
