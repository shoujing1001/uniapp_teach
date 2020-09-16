<template>
	<view>
		<view class="grid col-2">
			<view class="flex align-center">
				<image src="../../static/appicon.png" mode="aspectFill" class="course-round round margin-sm"></image>
				<view style="line-height: 1.5;">
					<view class="text-xl text-bold text-black">4312</view>
					<view class="text-gray text-cut">总参与人数（人）</view>
				</view>
			</view>
			<view @click="nav(1)" class="flex align-center">
				<image src="../../static/appicon.png" mode="aspectFill" class="course-round round margin-sm"></image>
				<view style="line-height: 1.5;">
					<view class="text-xl text-bold text-black flex align-center">64 <text class="icon-right text-gray margin-left-xs" style="font-size: 24upx;"></text></view>
					<view class="text-gray text-cut">已创建课程（个）</view>
				</view>
			</view>
			<view @click="nav(2)" class="flex align-center">
				<image src="../../static/appicon.png" mode="aspectFill" class="course-round round margin-sm"></image>
				<view style="line-height: 1.5;">
					<view class="text-xl text-bold text-black flex align-center">43<text class="icon-right text-gray margin-left-xs" style="font-size: 24upx;"></text></view>
					<view class="text-gray text-cut">我的题库（个）</view>
				</view>
			</view>
			<view @click="nav(3)" class="flex align-center">
				<image src="../../static/appicon.png" mode="aspectFill" class="course-round round margin-sm"></image>
				<view style="line-height: 1.5;">
					<view class="text-xl text-bold text-black flex align-center">6875<text class="icon-right text-gray margin-left-xs" style="font-size: 24upx;"></text></view>
					<view class="text-gray text-cut">今日收益（元）</view>
				</view>
			</view>
		</view>
		<view class="margin-sm padding-lr-sm text-xl text-black" style="border-left: #ffd400 solid 8upx;">
			待完成课程
		</view>
		<view @click="toCourseDetail(1)" class="margin-sm padding-sm bg-gray" style="border-radius: 15upx;">
			<view class="flex justify-between">
				<image src="../../static/logo.png" mode="aspectFill" class="margin-right-sm" style="width: 200upx;height: 220upx;border-radius: 15upx;"></image>
				<view class="padding-right-sm flex flex-direction justify-between padding-tb-sm">
					<view class="text-xl text-bold text-black">理解孩子的需求</view>
					<view class="text-black">80%的家长都不理解孩子的思维</view>
					<view class="text-grey text-cut"><text>王教授</text><text class="margin-lr-xs">|</text><text>北京师范大学幼儿教育讲师</text></view>
					<view class="text-grey text-bold"><text>共21章节</text><text class="margin-lr-xs">已进行 3 节</text></view>
				</view>
			</view>
			<view class="margin-top-sm round ing-bg flex align-center padding-lr-sm" style="line-height: 1.6;">
				<view class="icon-timefill text-yellow"></view>
				<view class="text-lg text-white padding-left-xs">正在进行：线下交流会</view>
			</view>
		</view>
		<view v-for="(item,index) in courseList" :key="index" @click="toCourseDetail(1)"  class="margin-sm padding-sm bg-gray" style="border-radius: 15upx;">
			<view class="flex justify-between">
				<image src="../../static/logo.png" mode="aspectFill" class="margin-right-sm" style="width: 200upx;height: 230upx;border-radius: 15upx;"></image>
				<view class="padding-right-sm flex flex-direction justify-between padding-tb-sm">
					<view class="text-xl text-bold text-black">理解孩子的需求</view>
					<view class="text-black">80%的家长都不理解孩子的思维</view>
					<view class="text-grey text-cut"><text>王教授</text><text class="margin-lr-xs">|</text><text>北京师范大学幼儿教育讲师</text></view>
					<view class="text-grey text-bold"><text>共21章节</text><text class="margin-lr-xs">已进行 3 节</text></view>
				</view>
			</view>
			<view class="margin-top-sm round bg-white flex align-center padding-lr-sm" style="line-height: 1.6;">
				<view class="icon-timefill text-yellow"></view>
				<view class="text-lg padding-left-xs">正在进行：线下交流会</view>
			</view>
		</view>
		<view class="cu-bar"></view>
		<view class="solid-top bg-white padding-tb-xs flex align-center justify-center" style="position: fixed;bottom: 0;width: 100%;">
			<button @click="addCourse" class="cu-btn bg-gradual-orange round lg" style="width: 80%;">创建新课程</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				courseList:['a','b','c','d','e','f','g']//模拟课程列表
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
			addCourse(){
				uni.navigateTo({
					url:"../teacher_add_course/teacher_add_course"
				})
			},
			nav(index){
				var url = '';
				switch (index){
					case 0:
						break;
					case 1:url='../teacher_course_list/teacher_course_list'
						break;
					case 2:url='../teacher_tiku/teacher_tiku'
						break;
					case 3:url='../teacher_income_list/teacher_income_list'
						break;
					default:
						break;
				}
				uni.navigateTo({
					url:url
				})
			},
			toCourseDetail(id){
				//根据id跳转或整个item传递到详情页
				uni.navigateTo({
					url:"../teacher_course_detail/teacher_course_detail?id="+id
				})
			},
			getData(){
				const that = this
				uni.showLoading({
					title:"获取数据中..."
				})
				//接口获取数据，回调中处理
				setTimeout(function() {
					that.courseList = that.courseList.concat(that.courseList);
					uni.hideLoading();
				}, 1000*2);
			}
		}
	}
</script>

<style>
	.course-round{
		width: 120upx;
		height: 120upx;
	}
	.ing-bg{
		background-color: #ff8984;
	}
</style>
