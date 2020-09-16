<template>
	<view>
		<view v-for="(item,index) in tikuList" :key="index" class="margin-sm padding-sm bg-gray" style="border-radius: 10upx;">
			<view class="text-black text-lg">这个是题目标题，这个是题目标题</view>
			<view class="flex justify-between align-center padding-top-sm">
				<view class="text-grey">创建于 2019-12-24</view>
				<view class="flex">
					<view @click="nav" class="cu-btn line-orange margin-right-sm round ">编辑</view>
					<view @click="delet" class="cu-btn line-red round">删除</view>
				</view>
			</view>
		</view>
		<!-- 自定义弹窗 -->
		<uni-popup ref="popup" type="center" :custom="true">
			<view class="bg-white " style="padding-top: 50rpx;padding-bottom: 50rpx;width: 670rpx;border-radius: 15rpx;">
				<view class="padding  text-center text-black text-bold text-lg" style="line-height: 1.8;">
					是否确认删除题目
				</view>
				<view class="cu-bar btn-group padding-lr-sm padding-tb">
					<button @click="cancel" class="bg-gradual-gray cu-btn round lg">取消</button>
					<button @click="submit" class="bg-gradual-orange cu-btn round lg" style="width: 188rpx;">确认删除</button>
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
				tikuList:['a','b','c','d','e','f','g','h','i','j']//模拟题目列表
			}
		},
		onLoad() {
			this.getData();
		},
		onReachBottom() {
			this.pageIndex ++;
			this.getData();
		},
		components: {uniPopup},
		methods: {
			delet(){
				// 弹窗提醒 popup组件文档 https://ext.dcloud.net.cn/plugin?id=329
				this.$refs.popup.open()
			},
			nav(){
				uni.navigateTo({
					url:"../teacher_tiku_add/teacher_tiku_add"
				})
			},
			cancel(){
				//取消删除
				//关闭弹窗
				this.$refs.popup.close()
			},
			submit(){
				//确认删除
				this.$refs.popup.close()
			},
			getData(){
				const that = this
				uni.showLoading({
					title:"获取数据中..."
				})
				//接口获取数据，回调中处理
				setTimeout(function() {
					that.tikuList = that.tikuList.concat(that.tikuList);
					uni.hideLoading();
				}, 1000*2);
			}
		}
	}
</script>

<style>

</style>
