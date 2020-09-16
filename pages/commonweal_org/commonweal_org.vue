<template>
	<view>
		<view class="flex align-center justify-center flex-direction padding-tb">
			<image src="../../static/logo.png" mode="aspectFill" class="round" style="width: 150rpx;height: 150rpx;"></image>
			<view class="text-black text-xl text-bold padding-tb-sm">中国少儿慈善机构</view>
			<view class="text-gray ">已在民政部注册公墓资治资格的慈善组织</view>
		</view>
		<view class="margin-lr-sm padding-lr-sm text-lg text-bold text-black" style="border-left: #ffd400 solid 8upx;">
			公益项目
		</view>
		<scroll-view scroll-x="true">
			<view class="flex padding-top-sm padding-bottom">
				<view v-for="(item,index) in 5" :key="index" @click="toTopic(item)"
				class="padding-lr-sm">
					<image src="../../static/logo.png" mode="aspectFill" 
					style="width: 300upx;height: 200upx;border-radius: 15upx;"></image>
					<view style="width: 300rpx;" class="text-black padding-top-xs text-cut "
					>贫困山区资助活动</view>
				</view>
			</view>
		</scroll-view>
		<view class="margin-lr-sm padding-lr-sm text-lg text-bold text-black" style="border-left: #ffd400 solid 8upx;">
			组织信息
		</view>
		<view class="padding-left padding-top padding-bottom-sm">
			<view class="padding-bottom-sm">
				<view class="text-sm text-grey">成立时间</view>
				<view class="text-black padding-top-xs">2012.02.06</view>
			</view>
			<view class="padding-bottom-sm">
				<view class="text-sm text-grey">组织规模</view>
				<view class="text-black padding-top-xs">全职32人</view>
			</view>
			<view class="padding-bottom-sm">
				<view class="text-sm text-grey">联系地址</view>
				<view class="text-black padding-top-xs">广东省东莞市</view>
			</view>
			<view class="padding-bottom-sm">
				<view class="text-sm text-grey">联系电话</view>
				<view class="text-black padding-top-xs">0759-12423523</view>
			</view>
			<view class="padding-bottom-sm">
				<view class="text-sm text-grey">官方网站</view>
				<view class="text-black padding-top-xs">www.baidu.com</view>
			</view>
		</view>
		<view class="margin-lr-sm padding-lr-sm text-lg text-bold text-black" style="border-left: #ffd400 solid 8upx;">
			机构证书
		</view>
		<view class="padding-left padding-tb flex">
			<view v-for="(item,index) in 3" :key="index" class="padding-right-sm">
				<image src="../../static/logo.png" mode="aspectFill" style="width: 216rpx;height: 300rpx;"></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
	page{
		background-color: #fff;
	}

</style>
