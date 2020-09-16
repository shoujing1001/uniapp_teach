<template>
	<view>
		<view class="padding-tb text-xl text-black solid-top solid-bottom padding-lr-sm">
			<text class="text-orange">3.</text><text>地点1</text>
		</view>
		<!-- 表单 -->
		<view class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
			<view >第1章节<text class="text-red">*</text></view>
			<input class="text-right" type="text" placeholder="请输入章节标题" />
		</view>
		<view class="padding-tb solid-bottom solid-top padding-lr-sm">
			<view >章节简介<text class="text-red">*</text></view>
			<textarea class="padding-tb-sm" placeholder="请输入章节简介" />
		</view>
		<view @click="selectType" class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
			<view >趣跑类型<text class="text-red">*</text></view>
			<view class=""><text>{{type[typeIndex]}}</text><text class="icon-right margin-left-xs"></text></view>
		</view>
		<view class="padding-tb flex solid-bottom solid-top justify-between padding-lr-sm">
			<view >章节签到位置<text class="text-red">*</text></view>
			<view v-if="address" class="flex">
				<view style="width: 400upx;" class="text-black text-cut">{{address}}</view>
				<view @click="chooseAddress" class="padding-lr-sm round line-orange" style="line-height: 1.6;border: #f37b1d solid 2upx;">重置</view>
			</view>
			<view v-if="!address" @click="chooseAddress">请选择地址</view>
		</view>
		<view @click="isPhoto" class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
			<view >是否需要拍照签到<text class="text-red">*</text></view>
			<view class=""><text>{{isphoto[isphotoIndex]}}</text><text class="icon-right margin-left-xs"></text></view>
		</view>
		<view @click="selectTime" class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
			<view >完成时间限制<text class="text-red">*</text></view>
			<view class=""><text>{{time[timeIndex]}}</text><text class="icon-right margin-left-xs"></text></view>
		</view>
		<view class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
			<view >章节完成积分<text class="text-red">*</text></view>
			<input style="flex-grow: 1;" class="text-right text-df" type="text" placeholder="请输入积分数,0表示不设置积分" />
		</view>
		<view @click="isJishi" class="padding-tb flex solid-bottom solid-top justify-between padding-lr-sm">
			<view >是否开启计时<text class="text-red">*</text></view>
			<view class=""><text>{{jishi[jishiIndex]}}</text><text class="icon-right margin-left-xs"></text></view>
		</view>
		<view @click="isAns" class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
			<view >是否需要答题<text class="text-red">*</text></view>
			<view class=""><text>{{ans[ansIndex]}}</text><text class="icon-right margin-left-xs"></text></view>
		</view>
		<!-- 题目区域 -->
		<view v-if="ansIndex == 0">
			<!-- 题型选择 -->
			<view class="flex text-gray padding-sm">
				<view @click="tiXing(0)" :class="[tiType == 0 ? 'solid-short text-black text-bold' : '']" class="margin-right-sm" style="line-height: 1.8;">问答题</view>
				<view @click="tiXing(1)" :class="[tiType == 1 ? 'solid-short text-black text-bold' : '']" class="margin-right-sm" style="line-height: 1.8;">选择题</view>
				<view @click="tiXing(2)" :class="[tiType == 2 ? 'solid-short text-black text-bold' : '']" style="line-height: 1.8;">应用题库</view>
			</view>
			<!-- 第一类题型 -->
			<view v-if="tiType == 0">
				<view class="padding-tb padding-lr-sm solid-bottom solid-top">
					<input type="text" placeholder="请输入你的问题标题" />
				</view>
				<view class="padding-tb padding-lr-sm solid-bottom solid-top">
					<input type="text" placeholder="请输入你的问题介绍" />
				</view>
				<view class="padding-tb padding-lr-sm solid-bottom solid-top">
					<input type="text" placeholder="请输入你的答案" />
				</view>
				<view class="padding-sm" style="width: 100%;">
					<view class="text-bold text-black padding-tb-sm">添加图片内容({{picNum}}/1)</view>
					<view v-if="tiPic == ''" @click="choosePic" class="flex align-center justify-center" style="width: 33.3%;height: 200upx;border: #999999 dashed 2upx;">
						<view class="icon-camera" style="font-size: 80upx;"></view>
					</view>
					<view v-if="tiPic" @click="choosePic" class="flex align-center justify-center bg-img" 
					style="width: 33.3%;height: 200upx;"
					:style="'background-image:url('+tiPic+')'"></view>
				</view>
			</view>
			<!-- 第二类题型 -->
			<view v-if="tiType == 1">
				<view class="padding-tb padding-lr-sm solid-bottom solid-top">
					<input type="text" placeholder="请输入你的问题标题" />
				</view>
				<view class="padding-tb padding-lr-sm solid-bottom solid-top">
					<input type="text" placeholder="请输入你的问题介绍" />
				</view>
				<view class="padding-tb padding-lr-sm solid-bottom solid-top">
					<input type="text" placeholder="答题积分 0表示无积分" />
				</view>
				<view class="padding-sm" style="width: 100%;">
					<view class="text-bold text-black padding-tb-sm">添加图片内容({{picNum}}/1)</view>
					<view v-if="tiPic == ''" @click="choosePic" class="flex align-center justify-center" style="width: 33.3%;height: 200upx;border: #999999 dashed 2upx;">
						<view class="icon-camera" style="font-size: 80upx;"></view>
					</view>
					<view v-if="tiPic" @click="choosePic" class="flex align-center justify-center bg-img" 
					style="width: 33.3%;height: 200upx;"
					:style="'background-image:url('+tiPic+')'"></view>
				</view>
				<view v-if="xuanxiangNum >= 1" class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
					<view >选项一</view>
					<input class="text-right" type="text" placeholder="请输入选项内容" />
				</view>
				<view v-if="xuanxiangNum >= 2" class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
					<view >选项二</view>
					<input class="text-right" type="text" placeholder="请输入选项内容" />
				</view>
				<view v-if="xuanxiangNum >= 3" class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
					<view >选项三</view>
					<input class="text-right" type="text" placeholder="请输入选项内容" />
				</view>
				<view v-if="xuanxiangNum <= 3" class="solid-top padding-tb flex align-center justify-center">
					<button @click="addSelcet" class="cu-btn round" style="width: 90%;">添加选项（{{xuanxiangNum}}/3）</button>
				</view>
				<view class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
					<view >选项答案<text class="text-red">*</text></view>
					<input class="text-right" type="text" placeholder="请输入选项答案" />
				</view>
			</view>
			<!-- 第三类题型 -->
			<view v-if="tiType == 2">
				<view class="text-black text-bold padding-sm">应用题库</view>
				<view @click="selectYingyong(0)" class="margin-sm padding-sm bg-gray" style="border-radius: 15upx;">
					<view class="flex padding-bottom-sm align-center justify-between">
						<view class="flex align-center">
							<view class="round" style="font-size: 40upx;" :class="[yingyong == 0 ? 'icon-roundcheckfill text-orange' : 'icon-round line-orange']"></view>
							<view class="padding-left-sm text-bold text-black">这个是题目标题，这个是题目标题</view>
						</view>
						<view class="icon-right"></view>
					</view>
					<view v-if="yingyong == 0">
						<textarea class="padding-tb-sm" placeholder="答题积分 0表示无积分" />
					</view>
				</view>
				<view @click="selectYingyong(1)" class="margin-sm padding-sm bg-gray" style="border-radius: 15upx;">
					<view class="flex padding-bottom-sm align-center justify-between">
						<view class="flex align-center">
							<view class="round" style="font-size: 40upx;" :class="[yingyong == 1 ? 'icon-roundcheckfill text-orange' : 'icon-round line-orange']"></view>
							<view class="padding-left-sm text-bold text-black">这个是题目标题，这个是题目标题</view>
						</view>
						<view class="icon-right"></view>
					</view>
					<view v-if="yingyong == 1">
						<textarea class="padding-tb-sm" placeholder="答题积分 0表示无积分" />
					</view>
				</view>
				<view @click="selectYingyong(2)" class="margin-sm padding-sm bg-gray" style="border-radius: 15upx;">
					<view class="flex padding-bottom-sm align-center justify-between">
						<view class="flex align-center">
							<view class="round" style="font-size: 40upx;" :class="[yingyong == 2 ? 'icon-roundcheckfill text-orange' : 'icon-round line-orange']"></view>
							<view class="padding-left-sm text-bold text-black">这个是题目标题，这个是题目标题</view>
						</view>
						<view class="icon-right"></view>
					</view>
					<view v-if="yingyong == 2">
						<textarea class="padding-tb-sm" placeholder="答题积分 0表示无积分" />
					</view>
				</view>
			</view>
		</view>
		<view class="cu-bar"></view>
		<view class="solid-top bg-white padding-tb-xs flex align-center justify-center" style="position: fixed;bottom: 0;width: 100%;">
			<!-- bg-gradual-orange背景色的渐变在naui.css这个文件中定义的，色值可能取得不准 -->
			<button class="cu-btn bg-gradual-orange round lg" style="width: 80%;">保存</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				type:['户外型','室内型'],
				typeIndex:0,
				address:'',
				isphoto:['是','否'],
				isphotoIndex:0,
				time:['半小时','一小时','两小时'],
				timeIndex:0,
				jishi:['是','否'],
				jishiIndex:0,
				ans:['是','否'],
				ansIndex:0,
				tiType:0,
				tiPic:'',
				picNum:0,
				xuanxiangNum:0,
				yingyong:0
			}
		},
		methods: {
			selectType(){
				const that = this;
				uni.showActionSheet({
				    itemList: this.type,
				    success: function (res) {
						that.typeIndex = res.tapIndex;
				    }
				});
			},
			chooseAddress(){
				const that = this;
				uni.chooseLocation({
				    success: function (res) {
						console.log(res)
						that.address = res.address
				    }
				});
			},
			isPhoto(){
				const that = this;
				uni.showActionSheet({
				    itemList: this.isphoto,
				    success: function (res) {
						that.isphotoIndex = res.tapIndex;
				    }
				});
			},
			selectTime(){
				const that = this;
				uni.showActionSheet({
				    itemList: this.time,
				    success: function (res) {
						that.timeIndex = res.tapIndex;
				    }
				});
			},
			isJishi(){
				const that = this;
				uni.showActionSheet({
				    itemList: this.jishi,
				    success: function (res) {
						that.jishiIndex = res.tapIndex;
				    }
				});
			},
			isAns(){
				const that = this;
				uni.showActionSheet({
				    itemList: this.ans,
				    success: function (res) {
						that.ansIndex = res.tapIndex;
				    }
				});
			},
			tiXing(index){
				this.tiType = index
			},
			choosePic(){
				const that = this;
				uni.chooseImage({
				    count: 1, //默认9
				    sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
				    sourceType: ['album'], //从相册选择
				    success: function (res) {
				        console.log(JSON.stringify(res.tempFilePaths));
						that.tiPic = res.tempFilePaths[0];
						that.picNum = 1;
				    }
				});
			},
			addSelcet(){
				this.xuanxiangNum ++;
			},
			selectYingyong(index){
				this.yingyong = index
			}
		}
	}
</script>

<style>
	page{
		background-color: #fff;
	}
	.solid-short{
		border-bottom: #fdb012 solid 2upx;
	}

</style>
