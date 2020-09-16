<template>
	<view>
		<!-- 顶部背景 -->
		<view class="top-bg" style="width: 750upx;height: 150upx;"></view>
		<view class="padding-tb padding-lr-sm flex justify-between" style="margin-top: -150upx;">
			<image src="../../static/logo.png" mode="aspectFill" class="margin-right-sm" style="width: 200upx;height: 220upx;border-radius: 15upx;"></image>
			<view class="padding-top-sm padding-bottom-xs flex justify-between flex-direction">
				<view class="text-xl text-bold text-black">理解孩子的需求，他们需要的是一门兴趣</view>
				<view class="flex justify-between align-center">
					<view class="">
						<view class="text-lg"><text class="text-red">已学3节</text><text class="text-grey margin-left-xs">21章节</text></view>
						<view class="text-grey text-sm">线下课程</view>
					</view>
					<view @click="collect" class="cu-btn bg-gradual-orange round">收藏课程</view>
				</view>
			</view>
		</view>
		<view class="padding-lr-sm padding-tb">
			中共中央总书记、国家主席、中央军委主席习近平14日下午在人民大会堂同各民主党派中央、全国工商联负责人和无党派人士代表欢聚一堂，共迎佳节。
		</view>
		<view class="margin-lr-sm flex justify-between padding-bottom">
			<view class="flex align-center">
				<image class="round" style="width: 40upx;height: 40upx;" src="../../static/appicon.png" mode="aspectFill"></image>
				<view class="text-grey padding-left-sm text-cut">
					王教授 | 师范大学幼儿教育讲师
				</view>
			</view>
		</view>
		<view class="padding-lr-sm flex justify-between top-bg padding-tb-sm align-center">
			<view class="text-red text-cut">
				课程截止时间：2019-12-25
			</view>
			<view class="flex align-center padding-left-sm">
				<view class="text-cut"><text>2398</text>人正在参与</view>
				<view class="cu-avatar-group" style="flex-shrink: 0;">
					<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view>
					<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81005.jpg);"></view>
				</view>
			</view>
		</view>
		<view class="padding-lr-sm margin-top-sm flex align-center padding-bottom-sm">
			<image src="../../static/appicon.png" mode="aspectFill" style="height: 40upx;width: 40upx;border-radius: 10upx;"></image>
			<view class="padding-left-sm">课程费12%将捐赠给爱心公益</view>
		</view>
		<view class="padding-lr-sm flex justify-between padding-bottom solid-bottom">
			<image src="../../static/logo.png" mode="aspectFill" style="width: 300upx;height: 200upx;border-radius: 15upx;"></image>
			<view class="padding-tb padding-left-sm flex justify-between flex-direction" style="flex-grow: 1;">
				<view class="text-lg text-black text-bold">贫困山区资助活动</view>
				<view class="flex align-center text-grey justify-between">
					<view class="flex align-center">
						<view class="text-cut"><text>6583</text>人帮助了我们</view>
						<view class="cu-avatar-group" style="flex-shrink: 0;">
							<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view>
							<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81005.jpg);"></view>
						</view>
					</view>
					<view class="icon-right"></view>
				</view>
				<view class="text-grey">已募集5630.00元</view>
			</view>
		</view>
		<view class="margin-lr-sm margin-tb padding-lr-sm text-xl text-black" style="border-left: #ffd400 solid 8upx;">
			课程章节
		</view>
		<view class="padding-left padding-right-xs">
			<view class="padding-bottom-sm text-xl text-black" style="line-height: 1.5;font-size: 28upx;">
				<view class="text-lg text-bold"><text class="text-orange">1.</text><text>松山湖松湖烟湖3km</text></view>
				<view class="text-lines-2-cut text-grey">
					凉山之行第二天，习近平总书记在成都主持召开打好精准脱贫攻坚战座谈会，强调提高脱贫质量，聚焦深贫地区，扎扎实实把脱贫攻坚战推向前进。要强化监管，做到阳光扶贫、廉洁扶贫。对扶贫领域腐败问题，发现一起严肃查处问责一起，绝不姑息迁就。
				</view>
				<view class="grid col-3 padding-top-sm">
					<view class="padding-right-sm">
						<image src="../../static/appicon.png" mode="aspectFill" style="height: 200upx;border-radius: 10upx;"></image>
					</view>
					<view class="padding-right-sm">
						<image src="../../static/appicon.png" mode="aspectFill" style="height: 200upx;border-radius: 10upx;"></image>
					</view>
					<view class="padding-right-sm">
						<image src="../../static/appicon.png" mode="aspectFill" style="height: 200upx;border-radius: 10upx;"></image>
					</view>
				</view>
			</view>
			<view class="flex align-center text-grey justify-between padding-right-sm margin-bottom">
				<view class="flex align-center">
					<view class="text-cut"><text>658</text>人已打卡</view>
					<view class="cu-avatar-group" style="flex-shrink: 0;">
						<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view>
						<view class="cu-avatar round sm" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81005.jpg);"></view>
					</view>
				</view>
			</view>
		</view>
		<view class="cu-bar"></view>
		<view class="cu-bar"></view>
		<view class="bg-white" style="position: fixed;bottom: 0;width: 100%;">
			<view class="cu-bar justify-center bg-green">
				购买后2元将捐赠 爱心公益 贫困山区资助行动
			</view>
			<view class="flex justify-between align-center padding-sm">
				<view class="">
					<text class="text-red">￥99.00</text>
					<text class="margin-left-sm">21 章节</text>
				</view>
				<button class="cu-btn bg-gradual-orange round lg">购买课程</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			collect(){
				uni.showToast({
					title:"收藏逻辑"
				})
			},
			more(){
				uni.showToast({
					title:"查看更多"
				})
			}
		}
	}
</script>

<style>
	.top-bg {
		background-color: #fffae8;
	}
	
	.text-lines-2-cut{
		overflow : hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 2;
		-webkit-box-orient: vertical;
	}

</style>
