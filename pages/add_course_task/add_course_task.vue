<template>
	<view>
		<view class="padding-tb text-xl text-black solid-top solid-bottom padding-lr-sm">
			<text class="text-orange">3.</text><text>任务1</text>
		</view>
		<!-- 表单 -->
		<view class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
			<view >第1章节<text class="text-red">*</text></view>
			<input v-model="title" class="text-right text-df" type="text" placeholder="请输入章节标题" />
		</view>
		<view class="padding-tb solid-bottom solid-top padding-lr-sm">
			<view >章节简介<text class="text-red">*</text></view>
			<textarea class="padding-tb-sm text-df" placeholder="请输入章节简介" />
		</view>
		<view class="padding-tb solid-top padding-lr-sm flex justify-between">
			<view >章节简介<text class="text-red">*</text></view>
			<view class="text-gray">点击图片重新上传</view>
		</view>
		<view class="solid-bottom flex flex-wrap padding-lr-xs padding-bottom" style="width: 750upx;line-break: normal;">
			<view style="position: relative;" v-for="(img,index) in absPicList" :key="index">
				<image :src="img" @click="chooseAbsPic(index)" mode="aspectFill" style="width: 225upx;height: 230upx;border: 10upx;" class="margin-xs"></image>
				<view @click.stop="delet(index)" class="bg-red round" style="position: absolute;top:-10upx;right: 0upx;padding-left: 10upx;padding-right: 10upx;line-height: 1.4;">×</view>
			</view>
			<!-- <image src="img" mode="aspectFill" style="width: 225upx;height: 230upx;border: 10upx;" class="margin-xs"></image> -->
			<view @click="chooseAbsPic(false)" class="flex align-center justify-center margin-xs" style="width: 225upx;height: 230upx;border: #999999 dashed 2upx;">
				<view class="icon-camera" style="font-size: 80upx;"></view>
			</view>
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
		<view class="solid-top bg-white padding-tb-xs flex align-center justify-center" style="position: fixed;bottom: 0;width: 100%;z-index: 9999;">
			<!-- bg-gradual-orange背景色的渐变在naui.css这个文件中定义的，色值可能取得不准 -->
			<button @click="save" class="cu-btn bg-gradual-orange round lg" style="width: 80%;">保存</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title:'',//章节标题
				abstract:'',//章节简介
				absPicList:[],//简介图片列表
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
			chooseAbsPic(index){
				uni.chooseImage({
				    count: 9, //默认9
				    sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
				    sourceType: ['album'], //从相册选择
				    success: (res) => {
				        console.log(JSON.stringify(res.tempFilePaths));
						if(!index){//没有索引，表示新增
							this.absPicList = this.absPicList.concat(res.tempFilePaths);
						}else{
							//有索引，表示替换
							this.absPicList[index] = res.tempFilePaths[0];//此处需要注意替换时只能替换一张图片，更保险的是在选择图片前判断一下index再确定可选择的图片数量
						}
				    }
				});
			},
			delet(index){
				this.absPicList.splice(index,1);
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
			},
			save(){
				
				//保存后退回上一页
				uni.navigateBack({
					delta:1
				})
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
