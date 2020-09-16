<template>
	<view>
		<view class="padding-tb flex justify-between text-xl text-black solid-top solid-bottom padding-lr-sm">
			<view >
				<text class="text-orange">2.</text><text>课程章节</text>
			</view>
			<!-- 添加按钮 -->
			<view @click="addChapter" class="cu-btn round line-orange" style="line-height: 1.6;">添加</view>
		</view>
		<view v-for="(item,index) in chapterList" :key="index" class="padding-tb padding-lr-sm solid-bottom align-center flex justify-between">
			<view class="flex">
				<text class="icon-sort" style="font-size: 40upx;"></text>
				<view class="margin-left-xs text-df">{{item.title}}</view>
			</view>
			<view class="flex align-center">
				<view class="flex align-center">
					<view class="margin-right-xs" :class="[item.isSet?'text-black':'text-gray']">{{item.isSet?'已设置':'未设置'}}</view>
					<view class="icon-right text-gray" style="font-size: 40upx;"></view>
				</view>
				<!-- 具体参数值请根据接口修改 -->
				<view @click="delet(index)" class="text-red flex align-center" v-if="courseType != '时间模式'">
					<view class="icon-deletefill" style="font-size: 40upx;"></view>
					<view class="margin-left-xs">删除</view>
				</view>
			</view>
		</view>
		<view v-if="courseType == '时间模式' && chapterList.length < 21" class="cu-bar justify-center solid-top text-gray">
			时间模式，课程章节必须为21天
		</view>
		<view class="cu-bar"></view>
		<view class="solid-top bg-white padding-tb-xs btn-group cu-bar " style="position: fixed;bottom: 0;width: 100%;">
			<button @click="save" class="cu-btn line-orange round lg">先保存</button>
			<button @click="next" class="cu-btn bg-gradual-orange round lg">下一步</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				courseType:'时间模式',
				chapterList:[
					
				],//任务列表
				
				
				
			}
		},
		//根据其他页面传值或请求接口获取课程类型，据此判断章节列表的展现形式
		onLoad(option) {
			//此处用选择表单代替，以便查看效果
			const itemList = ['任务模式','时间模式','地点模式'];
			uni.showActionSheet({
				itemList:itemList,
				success: (res) => {
					this.courseType = itemList[res.tapIndex];
				}
			})
		},
		methods: {
			//添加章节
			addChapter(){
				var tmpItem = {
					title:'',
					isSet:true
				};
				if(this.chapterList.length >= 2){
					tmpItem.isSet = false;
				}
				switch (this.courseType){
					case '任务模式':
						tmpItem.title = '任务'+ parseInt(this.chapterList.length+1);
						this.chapterList.push(tmpItem);
						break;
					case '时间模式':
						tmpItem.title = '第'+ parseInt(this.chapterList.length+1)+'天';
						this.chapterList.push(tmpItem);
						break;
					case '地点模式':
						tmpItem.title = '地点'+ parseInt(this.chapterList.length+1);
						this.chapterList.push(tmpItem);
						break;
				}
				console.log(this.chapterList)
			},
			//删除元素
			delet(index){
				this.chapterList.splice(index,1)
			},
			//保存
			save(){
				
			},
			//下一步
			next(){
				uni.navigateTo({
					url:"../add_course_task/add_course_task"
				})
			}
		}
	}
</script>

<style>

</style>
