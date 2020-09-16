<template>
	<view>
		<view style="position: relative;">
			<image src="https://s2.ax1x.com/2019/11/05/M9VGge.jpg" mode="aspectFill" style="width: 750rpx;height: 350rpx;"></image>
			<view @click="back" style="position: absolute;top: 80rpx;left:30rpx">
				<text class="icon-back text-white" style="font-size: 40rpx;"></text>
			</view>
			<view class="padding-sm flex justify-between" style="position: absolute;bottom: 0;width: 750rpx;">
				<button class="round cu-btn dona-btn">我已累计捐助13元</button>
				<button class="round cu-btn dona-btn">我的捐赠证书</button>
			</view>
		</view>
		<view class="padding-tb margin-lr-sm flex justify-between solid-bottom">
			<view class="text-center solid-right" style="flex-grow: 1;">
				<view class="text-black text-xxl text-bold">64863</view>
				<view class="text-df text-gray">已参与(人)</view>
			</view>
			<view class="text-center" style="flex-grow: 1;">
				<view class="text-black text-xxl text-bold">15895.00</view>
				<view class="text-df text-gray">已募集(元)</view>
			</view>
		</view>
		<view @click="showpop" class="padding-tb margin-lr solid-bottom">
			<view class=" flex align-center padding-bottom-sm">
				<view class="padding-right-sm text-lg text-black">贫困山区资助行动</view>
				<image src="../../static/logo.png" mode="aspectFill" style="height: 35upx;width: 35upx;border-radius: 10upx;"></image>
			</view>
			<view class=" flex align-center">
				<image class="round" style="width: 40upx;height: 40upx;" src="../../static/logo.png" mode="aspectFill"></image>
				<view class="text-grey padding-left-sm text-cut ">
					爱心公益组织<text class="icon-right margin-left-sm"></text>
				</view>
			</view>
		</view>
		<view class="margin-lr solid-bottom padding-tb">
			<view class=" flex align-center padding-bottom-sm">
				<image src="../../static/logo.png" mode="aspectFill" style="height: 55rpx;width: 55rpx;border-radius: 5000rpx;"></image>
				<view class="padding-left-sm">
					<view class="text-black text-lg">刘海峰 会长</view>
					<view class="text-gray">中国少儿慈善协会会长</view>
				</view>
			</view>
			<view class="cu-list grid col-2">
				<view class="text-left padding-top-sm padding-left-sm">
					<view class="text-black">立项编号</view>
					<view class="text-sm text-gray padding-top-sm">43745856857957</view>
				</view>
				<view class="text-left padding-top-sm padding-left-sm">
					<view class="text-black">立项编号</view>
					<view class="text-sm text-gray padding-top-sm">43745856857957</view>
				</view>
				<view class="text-left padding-top-sm padding-left-sm">
					<view class="text-black">立项编号</view>
					<view class="text-sm text-gray padding-top-sm">43745856857957</view>
				</view>
				<view class="text-left padding-top-sm padding-left-sm">
					<view class="text-black">立项编号</view>
					<view class="text-sm text-gray padding-top-sm">43745856857957</view>
				</view>
			</view>
		</view>
		<view class="margin-lr-sm padding-lr-sm margin-tb text-lg text-bold text-black" style="border-left: #ffd400 solid 8upx;">
			公益进展
		</view>
		<view class="margin-lr-sm">
			<view class="cu-timeline">
				<view class="cu-item icon-radioboxfill text-orange">
					<view class="text-lg flex align-center text-black">
						<view class="padding-right-sm">开始建设公共校园球场</view>
						<image src="../../static/juanzeng.png" mode="aspectFill" style="width: 35rpx;height: 35rpx;"></image>
					</view>
					<view class="text-df padding-top-xs text-grey">
						这是孩子们感谢哥哥姐姐送的画的一幅画
					</view>
					<view class="padding-top-xs">
						<image src="../../static/logo.png" mode="aspectFill" style="width: 680rpx;height: 300rpx;"></image>
					</view>
				</view>
				<view class="cu-item icon-radioboxfill text-orange">
					<view class="text-lg flex align-center text-black">
						<view class="padding-right-sm">项目立项</view>
					</view>
					<view class="text-df padding-top-xs text-grey">
						这是孩子们感谢哥哥姐姐送的画的一幅画
					</view>
					<view class="padding-top-xs">
						<image src="../../static/logo.png" mode="aspectFill" style="width: 680rpx;height: 300rpx;"></image>
					</view>
				</view>
				<view class="cu-item icon-radioboxfill text-orange">
					<view class="text-lg flex align-center text-black">
						<view class="padding-right-sm">项目立项</view>
					</view>
					<view class="text-df padding-top-xs text-grey">
						这是孩子们感谢哥哥姐姐送的画的一幅画
					</view>
					<view class="padding-top-xs">
						<image src="../../static/logo.png" mode="aspectFill" style="width: 680rpx;height: 300rpx;"></image>
					</view>
				</view>
			</view>
		</view>
		<view class="cu-bar"></view>
		<view class="solid-top bg-white padding-tb-xs flex align-center justify-center" style="position: fixed;bottom: 0;width: 100%;">
			<!-- bg-gradual-orange背景色的渐变在naui.css这个文件中定义的，色值可能取得不准 -->
			<button @click="donate" class="cu-btn bg-gradual-orange round lg" style="width: 90%;">捐助</button>
		</view>
		<!-- 自定义弹窗 -->
		<uni-popup ref="popup" type="center" :custom="true">
			<view class="bg-white " style="padding-top: 30rpx;padding-bottom: 30rpx;width: 670rpx;border-radius: 15rpx;">
				<view v-if="popupType == 1">
					<view class="text-center text-lg">公益透明提醒</view>
					<view class="padding-tb-sm margin-lr-sm solid-bottom text-lg text-black">款项讲捐赠给【贫困山区资助行动】</view>
					<view class="padding-lr-sm" style="padding-top: 60rpx;">
						<view class="text-gray">善款接收：中国少儿慈善基金会</view>
						<view class="text-gray">项目执行：中国少儿慈善基金会</view>
						<view class="text-gray">项目已执：已执行一个月</view>
					</view>
					<view class="padding-tb-sm padding-lr-sm">
						<text @click="check" 
						:class="[agree?'bg-white icon-round':'icon-roundcheckfill text-yellow']" 
						class="margin-right-xs"></text><text class="text-bold">同意</text><text
						 class="text-blue">《用户捐款协议》 </text>
					</view>
					<view class="cu-bar btn-group padding-lr-sm padding-tb">
						<button @click="more" class="bg-gradual-gray cu-btn round lg">了解更多</button>
						<button @click="checked" class="bg-gradual-orange cu-btn round lg" 
						style="width: 188rpx;">我已知情</button>
					</view>
				</view>
				<view v-if="popupType == 2">
					<view class="text-center">捐助金额</view>
					<!-- <view class="padding-tb-sm margin-lr-sm solid-bottom text-lg text-black">款项讲捐赠给【贫困山区资助行动】</view> -->
					<view  class="cu-bar btn-group padding-tb-sm">
						<button @click="selectMon(0)" :class="[monIndex == 0 ?'bg-gradual-orange':'bg-gray']" class="cu-btn round lg">10元</button>
						<button @click="selectMon(1)" :class="[monIndex == 1 ?'bg-gradual-orange':'bg-gray']" class="cu-btn round lg">50元</button>
						<button @click="selectMon(2)" :class="[monIndex == 2 ?'bg-gradual-orange':'bg-gray']" class="cu-btn round lg">100元</button>
					</view>
					<view class="solid-bottom flex align-center padding-tb-sm margin-lr-sm">
						<text class="text-bold margin-right-sm">￥</text>
						<input style="flex-grow: 1;" v-model="money" placeholder="请输入金额" type="number" class="text-df" />
					</view>
					<view v-if="money && money < 1" class="padding-sm text-red">
						捐赠金额不得低于1元
					</view>
					<view class="cu-bar btn-group padding-lr-sm padding-tb">
						<button @click="cancel" class="bg-gradual-gray cu-btn round lg">取消</button>
						<button @click="submitDonate" class="bg-gradual-orange cu-btn round lg" 
						style="width: 188rpx;">确定</button>
					</view>
				</view>
				<view v-if="popupType == 3">
					<view class="text-center">支付方式</view>
					<view style="min-height: 300rpx;">
						<view @click="pay"
						class="flex margin-lr-sm justify-between align-center padding-tb solid-bottom">
							<view class="flex align-center">
								<image src="../../static/wechat.png" mode="widthFix" style="width: 60rpx;height: 60rpx;"></image>
								<view class="padding-left-sm text-lg">微信</view>
							</view>
							<view class="icon-right"></view>
						</view>
					</view>
					
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
				agree:false,
				popupType:1,//1 公益透明提醒 2捐助 3支付方式
				monIndex:99,
				money:''
			}
		},
		components: {uniPopup},
		methods: {
			back(){
				uni.navigateBack({
					delta:1
				})
			},
			//捐赠协议
			showpop(){
				this.popupType = 1
				this.$refs.popup.open()
			},
			//同意协议
			check(){
				this.agree ? this.agree = false : this.agree = true
			},
			//捐助选择
			selectMon(index){
				this.monIndex = index
			},
			//了解捐赠更多
			more(){
				this.cancel()
			},
			//我已知晓
			checked(){
				this.cancel()
			},
			//打开捐赠窗
			donate(){
				this.popupType = 2
				this.$refs.popup.open()
			},
			//关闭弹窗
			cancel(){
				this.$refs.popup.close()
			},
			//确认支付
			submitDonate(){
				uni.showLoading({
					
				})
				// this.$refs.popup.close()
				this.popupType = 3
				setTimeout(function() {
					uni.hideLoading()
				}, 800);
				
			},
			//去支付页面
			pay(){
				this.$refs.popup.close()
			}
		}
	}
</script>

<style>
	page{
		background-color: #fff;
	}
	.dona-btn{
		background-color: rgba(255,255,255,0.8);
	}

</style>
