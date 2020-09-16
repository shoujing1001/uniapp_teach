<template>
	<view>
		<view class="padding-tb text-xl text-black solid-top solid-bottom padding-lr-sm">
			<text class="text-orange">4.</text><text>课程发布</text>
		</view>
		<view class="padding-tb solid-bottom solid-top  padding-lr-sm">
			<view class="flex justify-between align-center">
				<view >课程费用<text class="text-red">*</text></view>
				<view class="flex align-center">
					<input class="text-right text-df" type="text" placeholder="请设置课程费用"/>
					<view class="padding-left-sm">元</view>
				</view>
			</view>
			<view class="text-gray text-sm padding-top-sm">0表示免费课程</view>
		</view>
		<view class="padding-tb flex justify-between padding-lr-sm solid-bottom">
			<view>
				<view >课程封面<text class="text-red">*</text></view>
				<view class="text-gray text-sm padding-top-sm">点击图片可重新上传</view>
			</view>
			<view v-if="coverPic == ''" @click="chooseCoursePic" class="flex align-center justify-center margin-xs" style="width: 225upx;height: 230upx;border: #999999 dashed 2upx;">
				<view class="icon-camera" style="font-size: 80upx;"></view>
			</view>
			<view v-if="coverPic" @click="chooseCoursePic" class="flex align-center justify-center bg-img margin-xs"
			style="width: 225UPX;height: 230upx;"
			:style="'background-image:url('+coverPic+')'"></view>
		</view>
		<view class="padding-tb padding-lr-sm">
			<view class="text-black text-bold">课程费平台结算说明：</view>
			<view class="text-grey padding-tb-sm">
				课程费用将扣除10%作为公益募捐，剩余课程费用平台抽取20%后结算至账户
			</view>
		</view>
		<view class="cu-bar"></view>
		<view class="solid-top bg-white padding-tb-xs btn-group cu-bar " style="position: fixed;bottom: 0;width: 100%;">
			<button @click="save" class="cu-btn line-orange round lg">先保存</button>
			<button @click="confirm" class="cu-btn bg-gradual-orange round lg">确认发布</button>
		</view>
		<!-- 自定义弹窗 -->
		<uni-popup ref="popup" type="center" :custom="true">
			<view class="bg-white " style="padding-top: 50rpx;padding-bottom: 50rpx;width: 670rpx;border-radius: 15rpx;">
				<view class="padding  text-center text-black text-bold text-lg" style="line-height: 1.8;">
					老师，请您仔细检查课程<br/>一经发布后不可修改
				</view>
				<view class="cu-bar btn-group padding-lr-sm padding-tb">
					<button @click="cancel" class="bg-gradual-gray cu-btn round lg">取消</button>
					<button @click="submit" class="bg-gradual-orange cu-btn round lg" style="width: 188rpx;">确认发布</button>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	// 使用popup组件自定义弹窗
	import uniPopup from "@/components/uni-popup/uni-popup.vue"
	export default {
		data() {
			return {
				coverPic:'',//封面
			}
		},
		onLoad() {
			
		},
		components: {uniPopup},
		methods: {
			chooseCoursePic(){
				uni.chooseImage({
				    count: 1, 
				    sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
				    sourceType: ['album'], //从相册选择
				    success: (res) => {
				        this.coverPic = res.tempFilePaths[0];
				    }
				});
			},
			save(){
				
			},
			//确认发布
			confirm(){
				// 弹窗提醒 popup组件文档 https://ext.dcloud.net.cn/plugin?id=329
				this.$refs.popup.open()
			},
			cancel(){
				//取消发布
				//关闭弹窗
				this.$refs.popup.close()
			},
			submit(){
				//提交发布
				this.$refs.popup.close()
			}
		}
	}
</script>

<style>

</style>
