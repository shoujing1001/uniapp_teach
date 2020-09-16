<template>
	<view>
		<scroll-view scroll-x class="bg-white nav text-center solid-bottom">
			<view class="cu-item" :class="sIndex==0?'my-cur text-black text-bold':'text-gray'"  @tap="tabSelect(0)">
				选择题
			</view>
			<view class="cu-item" :class="sIndex==1?'my-cur text-black text-bold':'text-gray'"  @tap="tabSelect(1)">
				问答题
			</view>
		</scroll-view>
		<!-- 选择题 -->
		<view v-if="sIndex == 0" class="">
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
			<view v-if="xuanxiangNum < 3" class="solid-top padding-tb flex align-center justify-center">
				<button @click="addSelcet" class="cu-btn round" style="width: 90%;">添加选项（{{xuanxiangNum}}/3）</button>
			</view>
			<view class="padding-tb solid-bottom solid-top flex justify-between padding-lr-sm">
				<view >选项答案<text class="text-red">*</text></view>
				<input class="text-right" type="text" placeholder="请输入选项答案" />
			</view>
		</view>
		<!-- 问答题 -->
		<view v-if="sIndex == 1" class="">
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
		<view class="cu-bar"></view>
		<view class="solid-top bg-white padding-tb-xs btn-group cu-bar " style="position: fixed;bottom: 0;width: 100%;z-index: 9999;">
			<button @click="cancel" class="cu-btn bg-gradual-gray round lg">取消</button>
			<button @click="save" class="cu-btn bg-gradual-orange round lg">确认创建</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sIndex:0,
				xuanxiangNum:0,
				tiPic:'',
				picNum:0,
			}
		},
		methods: {
			tabSelect(index){
				this.sIndex = index
			},
			choosePic(){
				uni.chooseImage({
				    count: 1, //默认9
				    sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
				    sourceType: ['album'], //从相册选择
				    success: (res)=> {
						this.tiPic = res.tempFilePaths[0];
						this.picNum = 1;
				    }
				});
			},
			addSelcet(){
				this.xuanxiangNum ++;
			},
			cancel(){
				uni.navigateBack({
					delta:1
				})
			},
			save(){
				uni.navigateBack({
					delta:1
				})
			}
		}
	}
</script>

<style>
	.my-cur{
		border-bottom: #feab00 solid 5upx;
	}

</style>
