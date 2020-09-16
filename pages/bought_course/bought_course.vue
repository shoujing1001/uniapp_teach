<template>
	<view>
		<view v-for="(item,index) in list" :key="index" class="margin-sm padding-sm" style="border-radius: 15upx;background-color: #fafafa;">
			<view class="flex">
				<image src="../../static/logo.png" mode="aspectFill" class="margin-right-sm" style="width: 200upx;height: 220upx;border-radius: 15upx;"></image>
				<view class="padding-right-sm flex flex-direction justify-between padding-tb-xs">
					<view class="text-xl text-bold text-black">理解孩子的需求</view>
					<view class="text-black">订单号：16574988854</view>
					<view class="text-grey">购买日期：2019.06.03</view>
					<view class="text-red text-bold">￥199.00</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:10
			}
		},
		onReachBottom() {
			const that = this
			uni.showLoading({
				title:"加载中..."
			})
			setTimeout(function() {
				that.list += 10
				uni.hideLoading()
			}, 1000);
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
