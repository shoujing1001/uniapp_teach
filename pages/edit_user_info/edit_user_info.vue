<template>
	<view>
		<view class="flex justify-between align-center solid-bottom padding-tb padding-lr-sm">
			<view class="">头像</view>
			<image @click="chooseImg" :src="avatar" mode="aspectFill" style="width: 100upx;height: 100upx;" class="round"></image>
		</view>
		<view class="flex align-center solid-bottom padding-tb padding-lr-sm">
			<view class="padding-right-sm">昵称</view>
			<input :disabled="edit" type="text" v-model="nickName" class=" text-df text-gray"/>
		</view>
		<view class="flex align-center solid-bottom padding-tb padding-lr-sm">
			<view class="padding-right-sm">性别</view>
			<input :disabled="edit" type="text" v-model="gender" class=" text-df text-gray"/>
		</view>
		<view class="flex align-center solid-bottom padding-tb padding-lr-sm">
			<view class="padding-right-sm">出生年月</view>
			<picker mode="date" fields="month" @change="dateChange">
				<view>{{birth}}</view>
			</picker>
		</view>
		<view class="flex align-center solid-bottom padding-tb padding-lr-sm">
			<view class="padding-right-sm">职业</view>
			<input :disabled="edit" type="text" v-model="occupation" class=" text-df text-gray"/>
		</view>
		<!-- <view class="flex align-center solid-bottom padding-tb padding-lr-sm">
			<view class="padding-right-sm">简介</view>
			<input :disabled="edit"
			 maxlength="100" type="text" v-model="abstract" placeholder="请输入简介" class=" text-df text-gray"/>
		</view> -->
		<view class="padding-tb padding-lr-sm solid-bottom">
			<view class="padding-right-sm">简介 （{{abstract.length}}/100）</view>
			<textarea :disabled="edit" placeholder="请输入简介" v-model="abstract" class="padding-tb-sm text-df" />
		</view>
		<view class="cu-bar"></view>
		<view class="solid-top bg-white padding-tb-xs flex align-center justify-center" style="position: fixed;bottom: 0;width: 100%;">
			<button class="cu-btn bg-gradual-orange round lg" style="width: 80%;">保存</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				edit:false,//控制是否可以编辑输入框
				nickName:'夜空中最亮的星星',
				gender:'男',
				birth:'2000-06',
				occupation:'教师',
				abstract:'我就是我',
				bind:false,
				avatar:'../../static/logo.png'
			}
		},
		onLoad() {
			
		},
		methods: {
			chooseImg(){
				uni.chooseImage({
					count:1,
					success: (res) => {
						this.avatar = res.tempFilePaths[0]
					}
				})
			},
			dateChange(e){
				//效果自己改一下
				this.birth = e.detail.value.substr(0,e.detail.value.length-3)
				console.log(e)
			}
		}
	}
</script>

<style>

</style>
