<template>
	<view class="loaderMore">{{loaderText}}</view>
</template>

<script>
	export default  {
		props:{
			loaderText:String
		}
	}
</script>

<style>
	/* 上拉加载 */
	.loaderMore {
		text-align: center;
		color: #aaa;
		padding: 10upx;
	}
</style>
