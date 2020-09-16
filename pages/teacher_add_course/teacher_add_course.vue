<template>
	<view>
		<view class="padding-tb text-xl text-black solid-top solid-bottom padding-lr-sm">
			<text class="text-orange">1.</text><text>课程信息</text>
		</view>
		<view class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
			<view >课程名称({{title.length}}/15)<text class="text-red">*</text></view>
			<input v-model="title" class="text-right text-df" type="text" placeholder="请输入课程名称" />
		</view>
		<view @click="selectType" class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
			<view >课程类型<text class="text-red">*</text></view>
			<view class=""><text>{{type[typeIndex]}}</text><text class="icon-right margin-left-xs"></text></view>
		</view>
		<view @click="selectMode" class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
			<view >章节模式<text class="text-red">*</text></view>
			<view class=""><text>{{mode[modeIndex]}}</text><text class="icon-right margin-left-xs"></text></view>
		</view>
		<view class="padding-tb solid-bottom solid-top padding-lr-sm">
			<view >课程简介（{{abstract.length}}/350)<text class="text-red">*</text></view>
			<textarea v-model="abstract" class="padding-tb-sm" style="width: 100%;" maxlength="350" placeholder="请输入课程简介" />
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
				title:'',//课程名称
				type:['任务模式','时间模式','趣跑模式'],
				typeIndex:0,
				mode:['自由签到','顺序签到'],
				modeIndex:0,
				abstract:'',//简介
			}
		},
		methods: {
			selectType(){
				uni.showActionSheet({
				    itemList: this.type,
				    success: (res)=>{
						this.typeIndex = res.tapIndex;
				    }
				});
			},
			selectMode(){
				uni.showActionSheet({
					itemList:this.mode,
					success: (res) => {
						this.modeIndex = res.tapIndex;
					}
				})
			},
			//保存
			save(){
				
			},
			//下一步
			next(){
				uni.navigateTo({
					url:"../course_chapter/course_chapter"
				})
			}
		}
	}
</script>

<style>

</style>
