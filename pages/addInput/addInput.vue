<template>
	<view>
		<uni-nav-bar left-icon="arrowleft" :statusBar="true" right-text="发布" left-text="返回" @clickLeft="back" @clickRight="submitContent">
			<view class="flexCenter" @click="changeRoot">
				{{titleText}}
				<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
	export default {
		components: {
			uniNavBar
		},
		data() {
			return {
				titleText: '所有人可见',
				rootText: ['所有人可见', '仅自己可见']
			}
		},
		methods: {
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
					success: (res)=> {
						console.log(res.tapIndex)
						this.titleText = this.rootText[res.tapIndex]
					}
				});
			}
		}
	}
</script>

<style>

</style>
