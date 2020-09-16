<template>
	<view>
		<view class="cu-bar justify-center" :class="[bind?'bg-gray':'weixin-bg text-weixin-bind']">
			<view class="flex align-center">
				<image style="width: 50upx;height: 50upx;" class="round" src="../../static/logo.png" mode="aspectFill"></image>
				<view class=" padding-left-sm">{{bind?'已授权成功':'请绑定您的微信账户'}}</view>
			</view>
		</view>
		<view class="flex justify-between align-center solid-bottom padding-tb padding-lr-sm">
			<view class="">头像</view>
			<image src="../../static/appicon.png" mode="aspectFill" style="width: 100upx;height: 100upx;" class="round"></image>
		</view>
		<view class="flex justify-between align-center solid-bottom padding-tb padding-lr-sm">
			<view class="">昵称</view>
			<input :disabled="edit" type="text" v-model="nickName" class="text-right text-df text-black"/>
		</view>
		<view class="flex justify-between align-center solid-bottom padding-tb padding-lr-sm">
			<view class="">性别</view>
			<input :disabled="edit" type="text" v-model="gender" class="text-right text-df text-black"/>
		</view>
		<view class="flex justify-between align-center solid-bottom padding-tb padding-lr-sm">
			<view class="">出生年月</view>
			<input :disabled="edit" type="text" v-model="birth" class="text-right text-df text-black"/>
		</view>
		<view class="flex justify-between align-center solid-bottom padding-tb padding-lr-sm">
			<view class="">职业</view>
			<input :disabled="edit" type="text" v-model="occupation" class="text-right text-df text-black"/>
		</view>
		<view class="padding-tb padding-lr-sm solid-bottom">
			<view class="">简介</view>
			<textarea :disabled="edit" placeholder="请输入简介" v-model="abstract" class="padding-tb-sm text-df" />
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				edit:true,//控制是否可以编辑输入框
				nickName:'夜空中最亮的星星',
				gender:'男',
				birth:'2000-06',
				occupation:'教师',
				abstract:'我就是我',
				bind:false
			}
		},
		onLoad() {
			uni.showActionSheet({
				itemList:['选择查看微信是否已绑定的效果','已绑定','未绑定'],
				success: (res) => {
					res.tapIndex == 1 ? this.bind = true : this.bind = false
				}
			})
		},
		onNavigationBarButtonTap(e){
			uni.showToast({
				title:"点击了顶部按钮"
			})
		},
		methods: {
			
		}
	}
</script>

<style>
	.weixin-bg{
		background-color: #e6ffe9;
	}
	
	.text-weixin-bind{
		color: #48c656;
	}

</style>
