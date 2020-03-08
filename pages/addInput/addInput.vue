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
	</view>
</template>

<script>
	import upLoadImage from '../../components/common/upLoadImage.vue'
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
	export default {
		components: {
			uniNavBar,
			upLoadImage
		},
		data() {
			return {
				titleText: '所有人可见',
				rootText: ['所有人可见', '仅自己可见'],
				imageList:[]
			}
		},
		methods: {
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

</style>
