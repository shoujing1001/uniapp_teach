<template>
	<view>
		<view class="padding-lr">
			<view class="text text-xl padding-top-sm text-bold">登录</view>
			<view class="text-lg padding-tb-sm">您好同学，欢迎来到21节课</view>
		</view>
		<view class="padding margin flex bg-gray round align-center">
			<view class="padding-lr-sm solid-right">
				<picker @change="bindPickerChange" :value="index" :range="array">
					{{array[index]}}<text class="icon-triangledownfill margin-left-xs"></text>
				</picker>
			</view>
			<view class="padding-lr-sm"><input v-model="phone" style="width: 100%;" type="text" placeholder="请输入手机号" class="text-df" /></view>
		</view>
		<view class="padding margin flex bg-gray round align-center">
			<view style="flex-grow: 1;" class="padding-lr-sm"><input v-model="validateCode" type="text" style="width: 100%;" placeholder="请输入验证码" class="text-df" /></view>
			<view @click="getValidate" class="padding-lr-sm solid-left text-orange">{{show?"获取验证码":`已发送${count}s`}}</view>
		</view>
		<view class="cu-bar justify-center padding-lr" style="width: 100%;">
			<button :class="[phone&&validateCode?'bg-gradual-orange':'bg-gray']"
			 class="cu-btn lg round" style="width: 100%;padding-top: 45upx;padding-bottom: 45upx;">登录</button>
		</view>
		<view class="text-center padding-lr padding-tb-xl flex justify-between">
			<view @click="click1" class="">账号密码登录</view>
			<view @click="click2" class="">注册</view>
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
				phone:'',
				validateCode:'',
				array:['+86','+85','+101','+102'],
				index:0
			}
		},
		methods: {
			async getValidate(){
				if(!(/^1(3|4|5|7|8)\d{9}$/.test(this.phone))){ 
					uni.showToast({
						title:"请输入正确的手机号码",
						icon:"none"
					})
					return false; 
				}
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
			click1(){
				uni.showToast({
					title:"选择了账号密码登录",
					icon:"none"
				})
			},
			click2(){
				uni.navigateTo({
					url:"../register/register"
				})
			},
			bindPickerChange(e){
				this.index = e.target.value
			}
		}
	}
</script>

<style>

</style>
