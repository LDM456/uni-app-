<template>
	<view class="uni-tab-bar">
		<scroll-view scroll-x class="uni-swiper-tab">
			<block v-for="(item,index) in tabBars" :key="item.id">
				<view class="swiper-tab-list" :class="{'active':tabIndex == index}" @tap="changeIndex(index)">
					{{item.name}}
					<view class="swiper-tab-line"></view>
				</view>
			</block>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		props:{
			tabBars:Array,
			tabIndex:Number
		},
		methods:{
			changeIndex(index) {
				this.$emit('changeIndex',index)
			},
		}
	}
</script>

<style>
	.uni-swiper-tab {
		border-bottom: 2upx solid # #eeeeee;
	}
	
	.swiper-tab-list {
		color: #969696;
	}
	
	.swiper-tab-list.active {
		color: #343434;
	}
	
	.active .swiper-tab-line {
		width: 60upx;
		background: #fede33;
		border: 6upx solid #fede33;
		margin: auto;
		border-radius: 10upx;
	}
</style>
