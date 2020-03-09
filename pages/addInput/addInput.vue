<template>
	<view>
		<uni-nav-bar left-icon="arrowleft" :statusBar="true" right-text="发布" @clickLeft="back" @clickRight="submitContent">
			<view class="flexCenter" @click="changeRoot">
				{{titleText}}
				<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>
		<!-- 添加多行文本框 -->
		<view class="uni-textarea">
			<textarea @blur="bindTextAreaBlur" placeholder="说一句话吧~"></textarea>
		</view>
		<!-- 上传多图 -->
		<up-load-image @upload="upload"></up-load-image>
		<!-- 中间弹出层 -->
		<uni-popup ref="showpopup" :type="center" >
			<view class="popup-content">
				<view class="flexCenter">
					<image src="../../static/image/addinput.png" mode="widthFix"></image>
				</view>
				<view>1、涉及黄色、政治，广告及骚扰信息</view>
				<view>2、涉及人身攻击</view>
				<view>3、留联系方式，透露他人隐私</view>
				<view>一经核实将被封禁，情节严重者永久封禁</view>
				<button type="primary" @tap="closePopup">朕知道了</button>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from '../../components/uni-popup/uni-popup.vue'
	import upLoadImage from '../../components/common/upLoadImage.vue'
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
	export default {
		components: {
			uniNavBar,
			upLoadImage,
			uniPopup
		},
		data() {
			return {
				titleText: '所有人可见',
				rootText: ['所有人可见', '仅自己可见'],
				imageList:[],
				center:'center',
				isSaveFlag:false,//是否保存的标识
			}
		},
		mounted() {
			this.popupShow()
		},
		onBackPress() {
			if(!this.isSaveFlag){
				this.isSave()
				return true;
			}
		},
		methods: {
			// 是否保存草稿
			isSave(){
				uni.showModal({
					content:'是否保存为草稿',
					cancelText:'不保存',
					confirmText:'保存',
					success:(res)=> {
						if(res.confirm){
							console.log('保存')
						}else{
							console.log('不保存')
						}
						this.isSaveFlag = true
						uni.navigateBack({
							delta:1
						})
					}
				})
			},
			// 关闭弹层
			closePopup(){
				this.$refs['showpopup'].close()
			},
			// 显示弹层
			popupShow(){
				this.$nextTick(() => {
					this.$refs['showpopup'].open()
				})
			},
			// 删除图片
			delImage(index){
				uni.showModal({
				    title: '提示',
				    content: '是否删除该图片',
				    success: (res)=> {
				        if (res.confirm) {
				            this.imageList.splice(index,1)
				        } 
				    }
				});
			},
			// 文本框失焦
			bindTextAreaBlur(e) {
				console.log(e.detail.value)
			},
			// 返回按钮事件
			back() {
				uni.navigateBack({
					delta: 1
				})
			},
			// 发布事件
			submitContent() {
				console.log(456)
			},
			// 隐私权限
			changeRoot() {
				uni.showActionSheet({
					itemList: this.rootText,
					success: (res) => {
						console.log(res.tapIndex)
						this.titleText = this.rootText[res.tapIndex]
					}
				});
			},
			// 子传父-上传图片
			upload(arr){
				this.imageList = arr
			}
			
		}
	}
</script>

<style>
	.uni-textarea {
		/* border-bottom: 1upx solid #eee; */
	}
	.popup-content {
		/* #ifndef APP-NVUE */
		display: block;
		/* #endif */
		background-color: #fff;
		padding: 15px;
		font-size: 14px;
	}
	.popup-content image{
		width: 70%;
	}
	.popup-content button{
		color: #171606;
		background: #ffe934;
		margin: 10px 0 0 0;
	}
</style>
