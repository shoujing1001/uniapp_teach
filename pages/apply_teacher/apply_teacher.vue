<template>
	<view>
		<view class="padding-tb align-center solid-bottom flex justify-between padding-lr-sm">
			<view >姓名<text class="text-red">*</text></view>
			<input class="text-right text-df" type="text" placeholder="请输入你的真实姓名" />
		</view>
		<view class="padding-tb align-center solid-bottom flex justify-between padding-lr-sm">
			<view >所属机构<text class="text-red">*</text></view>
			<input style="flex-grow: 1;" class="text-right text-df" type="text" placeholder="是否有教育机构,院校或个人组织" />
		</view>
		<view class="padding-tb align-center solid-bottom flex justify-between padding-lr-sm">
			<view >所在地区<text class="text-red">*</text></view>
			<input class="text-right text-df" type="text" placeholder="请选择所在地区" />
		</view>
		<view class="padding-tb align-center solid-bottom flex justify-between padding-lr-sm">
			<view >身份证号<text class="text-red">*</text></view>
			<input class="text-right text-df" type="text" placeholder="请输入你的身份证号" />
		</view>
		<view class="padding-tb align-center solid-bottom padding-lr-sm">
			<view >身份证正反面照片<text class="text-red">*</text></view>
			<view class="flex justify-between">
				<view class="padding-lr padding-top" style="flex-grow: 1;">
					<image @click="chooseImg(0)" :src="imgList[0]?imgList[0]: '../../static/image/btn_1.png'" mode="aspectFill" style="width: 100%;height: 200rpx;"></image>
				</view>
				<view class="padding-lr padding-top " style="flex-grow: 1;">
					<image @click="chooseImg(1)" :src="imgList[1]?imgList[1]:'../../static/image/btn_2.png'" mode="aspectFill" style="width: 100%;height: 200rpx;"></image>
				</view>
			</view>
		</view>
		<view class="padding-tb  padding-lr-sm">
			<view >备注<text class="text-gray"></text>（{{abstract.length}}/50)</view>
			<textarea v-model="abstract" 
			class="padding-tb-sm text-df" style="width: 100%;" maxlength="50" placeholder="请输入备注信息" />
		</view>
		<view class="cu-bar"></view>
		<view class="solid-top bg-white padding-tb-xs flex align-center justify-center" style="position: fixed;bottom: 0;width: 100%;">
			
			<button class="cu-btn bg-gradual-orange round lg" style="width: 80%;">确定</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				imgList:[],
				abstract:''
			}
		},
		methods: {
			chooseImg(index){
				uni.chooseImage({
					count:1,
					success: (res) => {
						this.$set(this.imgList,index,res.tempFilePaths[0])
					}
				})
			},
		}
	}
</script>

<style>

</style>
