<template>
	<view>
		<view class="solid-bottom padding-bottom flex align-start" v-for="(item,index) in clockList" :key="index">
			<view class="padding-sm">
				<image src="../../static/appicon.png" mode="aspectFill" class="round" style="width: 100rpx;height: 100rpx;"></image>
			</view>
			<view style="flex-grow: 1;">
				<view class="flex justify-between align-center padding-tb-sm padding-right-sm" >
					<view >
						<view class="text-bold text-lg text-lg padding-tb-xs">{{item.userName}}</view>
						<view class="padding-tb-xs">{{item.clockTime}}</view>
					</view>
					<view @click="setExct(index)" class="flex align-center">
						<view class="round" style="font-size: 40upx;" :class="[ item.isExcellent ? 'icon-roundcheckfill text-orange' : 'icon-round line-orange']"></view>
						<view class="padding-left-sm text-black">设置为优秀打卡</view>
					</view>
				</view>
				<view class="">
					<image src="../../static/logo.png" mode="aspectFill" style="height: 150upx;width: 150upx;"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				clockList:[
					{
						userName:'刘同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:true
					},
					{
						userName:'黄同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:false
					},
					{
						userName:'刘同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:true
					},
					{
						userName:'黄同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:false
					},
					{
						userName:'刘同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:true
					},
					{
						userName:'黄同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:false
					},
					{
						userName:'刘同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:true
					},
					{
						userName:'黄同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:false
					},
					
					{
						userName:'刘同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:true
					},
					{
						userName:'黄同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:false
					},
					{
						userName:'刘同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:true
					},
					{
						userName:'黄同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:false
					},
					{
						userName:'刘同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:true
					},
					{
						userName:'黄同学',
						clockTime:'2019-12-13 13:29',
						isExcellent:false
					}
				],
				picList:['../../static/logo.png','../../static/logo.png','../../static/logo.png'],
				pageIndex:1,
				pageSize:20
			}
		},
		onLoad() {
			this.getData();
		},
		onReachBottom() {
			this.pageIndex ++;
			this.getData();
		},
		methods: {
			setExct(index){
				console.log(index)
				this.clockList[index].isExcellent ? this.clockList[index].isExcellent = false : this.clockList[index].isExcellent = true;
			},
			getData(){
				const that = this
				uni.showLoading({
					title:"获取数据中..."
				})
				//接口获取数据，回调中处理
				setTimeout(function() {
					that.clockList = that.clockList.concat(that.clockList);
					uni.hideLoading();
				}, 1000*2);
			}
		}
	}
</script>

<style>

</style>
