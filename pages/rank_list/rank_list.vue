<template>
	<view>
		<view class="flex align-center justify-center flex-direction padding-tb">
			<image src="../../static/appicon.png" mode="aspectFill"
			style="width: 100upx;height: 100upx;border-radius: 15upx;"></image>
			<view class="text-orange text-bold padding-tb-sm">TOP{{rank.length}}</view>
			<view class="text-lg text-black">热门亲子课</view>
		</view>
		<view v-for="(item,index) in rank" :key="index" class="padding-tb-sm">
			<view class="text-orange text-center">
				—————<text class="margin-lr-sm">TOP{{index+1}}</text>—————
			</view>
			<view class="margin-sm padding-sm" style="border-radius: 15upx;background-color: #f3f3f3;">
				<view class="flex">
					<image src="../../static/logo.png" mode="aspectFill" class="margin-right-sm" style="width: 200upx;height: 220upx;border-radius: 15upx;"></image>
					<view class="flex flex-direction justify-between padding-tb-sm">
						<view class="text-lg text-bold text-black">理解孩子的需求</view>
						<view class="text-black">80%的家长都不理解孩子的思维</view>
						<view class="text-grey text-cut">
							王教授 | 师范大学幼儿教育讲师
						</view>
						<view class="flex justify-between align-center">
							<view class="text-cut">
								<text class="text-red">￥99.00</text>
								<text class="margin-left-sm">21 章节</text>
							</view>
							<view class="flex align-center">
								<view class="text-cut text-grey"><text>2398</text>人正在参与</view>
								<view class="cu-avatar-group" style="flex-shrink: 0;">
									<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view>
									<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81005.jpg);"></view>
								</view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				rank:[{
					id:1
				},{
					id:2
				}]//排行榜对象
			}
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
