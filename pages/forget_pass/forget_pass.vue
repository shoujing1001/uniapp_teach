<template>
	<view>
		<view class="padding-tb margin-lr solid-bottom flex justify-between">
			<view class="text-black">原密码</view>
			<input class="text-right text-df" type="text" placeholder="请输入原密码" />
		</view>
		<view class="padding-tb margin-lr solid-bottom flex justify-between">
			<view class="text-black">短信验证码</view>
			<view style="flex-grow: 1;" class="padding-lr-sm"><input type="text" style="width: 100%;" placeholder="请输入验证码" class="text-df text-right" /></view>
			<view @click="getValidate" class="padding-left-sm solid-left text-orange">{{show?"获取验证码":`已发送${count}s`}}</view>
		</view>
		<view class="padding-tb margin-lr solid-bottom flex justify-between">
			<view class="text-black ">新密码</view>
			<input class="text-right text-df" type="text" placeholder="请输入新密码" />
		</view>
		<view class="padding-tb margin-lr solid-bottom flex justify-between">
			<view class="text-black">确认新密码</view>
			<input class="text-right text-df" type="text" placeholder="请输入新密码" />
		</view>
		<view class="cu-bar justify-center padding-lr" style="width: 100%;margin-top: 100upx;">
			<button class="cu-btn bg-gradual-orange lg round" style="width: 100%;">确定</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				show:true,
				timer:null,
				count:'',
				phone:''
			}
		},
		methods: {
			async getValidate(){
				//表单设计图未包含手机号字段，故不验证，如确不需要，请删除
				// if(!(/^1(3|4|5|7|8)\d{9}$/.test(this.phone))){ 
				// 	uni.showToast({
				// 		title:"请输入正确的手机号码",
				// 		icon:"none"
				// 	})
				// 	return false; 
				// }
				const TIME_COUNT = 60;
				if (!this.timer) {
					this.count = TIME_COUNT;
					this.show = false;
					//此处写提交获取验证码的请求
					
					this.timer = setInterval(() => {
						if (this.count > 0 && this.count <= TIME_COUNT) {
							this.count--;
						} else {
							this.show = true;
							clearInterval(this.timer);
							this.timer = null;
						}
					}, 1000)
				}
			},
		}
	}
</script>

<style>

</style>
