<template>
	<view>
		<!-- 自定义弹窗 -->
		<uni-popup ref="popup" type="center" :custom="true">
			<view class="bg-white " style="padding-top: 30rpx;padding-bottom: 30rpx;width: 670rpx;border-radius: 15rpx;">
				<view class="text-center">第一关：数灯笼</view>
				<view class="padding-tb-sm text-center text-lg text-black">数数这里到底有多少灯笼呢？</view>
				<view class="flex justify-center">
					<image src="../../static/logo.png" mode="aspectFill"
					 style="border-radius: 15upx;height: 300upx;width: 90%;"
					 ></image>
				</view>
				<view v-if="ansType == '输入'" class="solid-bottom padding-tb-sm text-center">
					<input placeholder="请输入你的答案" class="text-df text-center" />
				</view>
				<view v-if="ansType == '选择题'" class="cu-bar btn-group padding-tb-sm">
					<button @click="selectAns(0)" :class="[ansIndex == 0 ?'bg-gradual-orange':'bg-gray']" class="cu-btn round lg">4个</button>
					<button @click="selectAns(1)" :class="[ansIndex == 1 ?'bg-gradual-orange':'bg-gray']" class="cu-btn round lg">5个</button>
					<button @click="selectAns(2)" :class="[ansIndex == 2 ?'bg-gradual-orange':'bg-gray']" class="cu-btn round lg">6个</button>
				</view>
				<view v-if="ansIndex == 0" class="text-center text-red">答案错误啦！</view>
				<view class="cu-bar btn-group padding-lr-sm padding-tb">
					<button @click="cancel" class="bg-gradual-gray cu-btn round lg">取消</button>
					<button @click="submit" class="bg-gradual-orange cu-btn round lg" style="width: 188rpx;">提交</button>
				</view>
			</view>
		</uni-popup>
		<!-- 打卡提醒 -->
		<uni-popup ref="popup1" type="center" :custom="true">
			<view class="bg-white " style="padding-top: 60rpx;padding-bottom: 60rpx;width: 670rpx;border-radius: 15rpx;">
				<view v-if="clockType=='打卡'" class="flex justify-center align-center flex-direction">
					<image src="../../static/appicon.png" mode="aspectFill"
					style="width: 150upx;height: 150upx;"></image>
					<view class="text-lg text-black padding-tb">恭喜你，打卡成功啦~</view>
					<button style="width: 35%;" @click="clockSucc" class="cu-btn bg-gradual-orange round lg">好的</button>
				</view>
				<view v-if="clockType=='完成'" class="flex justify-center align-center flex-direction">
					<image src="../../static/appicon.png" mode="aspectFill"
					style="width: 150upx;height: 150upx;"></image>
					<view class="text-lg text-black padding-tb">你已完成本课程啦</view>
					<button style="width: 35%;" @click="clockSucc" class="cu-btn bg-gradual-orange round lg">好的</button>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from "@/components/uni-popup/uni-popup.vue"
	export default {
		data() {
			return {
				ansType:'选择题',
				ansIndex:9,
				clockType:'打卡'
			}
		},
		onLoad() {
			this.ansType = '选择题'
			// uni.showActionSheet({
			// 	itemList:['答题类型','选择题','输入'],
			// 	success: (res) => {
			// 		if(res.tapIndex == 1){
			// 			this.ansType = '选择题'
			// 		}else{
			// 			this.ansType = '输入'
			// 		}
			// 		this.$refs.popup.open()
			// 	}
			// })
		},
		onReady(){
			this.$refs.popup.open()
		},
		components: {uniPopup},
		methods: {
			cancel(){
				this.$refs.popup.close()
				uni.navigateBack({
					delta:1
				})
			},
			submit(){
				this.$refs.popup.close()
				uni.showActionSheet({
					itemList:['提醒类型','本次打卡完成','课程完成'],
					success: (res) => {
						if(res.tapIndex == 1){
							this.clockType = '打卡'
						}else{
							this.clockType = '完成'
						}
						this.$refs.popup1.open()
					}
				})
				
			},
			clockSucc(){
				//如果需要传递前一页数据，可以使用uni.$emit 在前一页onload里注册uni.$on监听
				uni.$emit('clockSucc',true)
				this.cancel()
			},
			//选择题答案
			selectAns(index){
				this.ansIndex = index;
			},
		}
	}
</script>

<style>

</style>
