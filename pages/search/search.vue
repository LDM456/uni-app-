<template>
	<view>
		sousou
	</view>
</template>

<script>
	export default {
		data(){
			return{
				
			}
		},
		// 监听原生标题导航按钮点击事件
		onNavigationBarButtonTap(e) {
			if(e.index == 0){
				uni.navigateBack({
					delta:1//降级，相当于返回
				})
			}
		},
		// 监听搜索框文本变化
		onNavigationBarSearchInputChanged(e){
			console.log(e.text)
		},
		// 监听点击搜索框按钮事件
		onNavigationBarSearchInputConfirmed(e){
			console.log(e.text)
		}			
		
	}
</script>

<style>
</style>
