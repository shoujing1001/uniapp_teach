<template>
	<view>
		<view v-for="(item,index) in list" :key="index" class="margin-lr-sm flex justify-between padding-tb-sm solid-bottom">
			<image src="../../static/logo.png" mode="aspectFill" style="width: 260upx;height: 180upx;border-radius: 15upx;"></image>
			<view class="padding-tb-sm padding-left-sm flex justify-between flex-direction" style="flex-grow: 1;">
				<view class="text-lg text-black text-bold">贫困山区资助活动</view>
				<view class="flex align-center text-grey justify-between">
					<view class="flex align-center">
						<view class="text-cut"><text>6583</text>人帮助了我们</view>
						<view class="cu-avatar-group" style="flex-shrink: 0;">
							<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view>
							<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81005.jpg);"></view>
						</view>
					</view>
					<view class="icon-right"></view>
				</view>
				<view class="text-grey">已募集5630.00元</view>
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
