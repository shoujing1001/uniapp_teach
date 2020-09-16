<template>
	<view>
		<view class="flex align-center justify-center flex-direction padding-tb">
			<image src="../../static/juanzeng.png" mode="aspectFill" style="width: 150rpx;height: 150rpx;"></image>
			<view class="text-black text-xl text-bold padding-tb-sm">感谢您献出的爱心</view>
			<view class="text-gray ">可以留意我们的公益动态了解情况哦</view>
		</view>
		<view class="margin-lr-sm padding-top-sm solid-bottom"></view>
		<view class="flex align-center justify-center flex-direction padding-tb-sm">
			<view class="text-black text-lg text-bold padding-tb-sm">获得公益证书</view>
			<image src="../../static/logo.png" mode="aspectFill" style="width: 500rpx;height: 600rpx;border-radius: 15rpx;"></image>
		</view>
		<view class="bg-white padding-tb btn-group cu-bar margin-lr-xl">
			<button @click="save" class="cu-btn bg-gradual-blue round lg">保存图片</button>
			<button @click="share" class="cu-btn bg-gradual-orange round lg">分享</button>
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
			save(){
				// #ifdef H5
				uni.showToast({
					title:"h5不支持保存接口"
				})
				// #endif
				uni.downloadFile({
					url:"http://qiniuoss.nauzone.cn/admin/201912/201912092225450258933.jpg",
					success:(res)=>{
						console.log(res)
						uni.saveImageToPhotosAlbum({
							filePath: res.tempFilePath,
							success: function () {
								uni.showToast({
									title:"保存成功"
								})
								console.log('save success');
							}
						});
						
					}
				})
			},
			share(){
				uni.showToast({
					title:"分享"
				})
			}
		}
	}
</script>

<style>
	page{
		background-color: #fff;
	}
	.bg-gradual-blue {
	  background-image: linear-gradient(0deg, #489afb, #6dcafd);
	  color: #fff;
	}

</style>
