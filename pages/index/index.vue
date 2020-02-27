<template>
	<view>
		<index-tab-bar :tabBars="tabBars" :tabIndex="tabIndex" @changeIndex="changeIndex"></index-tab-bar>
			<!-- :style="{height:swiperHeight+'px'}" -->
		<view class="uni-tab-bar">
			<swiper class="swiper" :current="tabIndex"  @change="changeTab" :style="{height:swiperHeight+'px'}">
				<swiper-item  class="swiper-item" v-for="(item,index) in newList" :key="index">
					<scroll-view scroll-y class="list">
						<index-list :list="item.list"></index-list> 
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import indexTabBar from '../../components/index/index-tabBar.vue'
	import indexList from '../../components/index/index-list.vue'
	export default {
		components: {
			indexList,
			indexTabBar
		},
		data() {
			return {
				swiperHeight: 0, //默认高度
				tabIndex: 1, //默认第一个
				tabBars: [{
					name: '关注',
					id: 'guanzhu'
				}, {
					name: '推荐',
					id: 'tuijian'
				}, {
					name: '体育',
					id: 'tiyu'
				}, {
					name: '热点',
					id: 'redian'
				}, {
					name: '财经',
					id: 'caijing'
				}, {
					name: '娱乐',
					id: 'yule'
				}],
				newList: [{
					list: [{
							userPic: '../../static/demo/demo5.jpg',
							userName: '昵称123',
							isAttention: false,
							titleText: '我是标题我是标题我是标题我是标题我是标题我是标题我是标题',
							isType: 'video',
							titlePic: '../../static/demo/datapic/28.jpg',
							playNumber: '235',
							palyTime: '1822',
							infoNum: {
								userFlag: '1', //0:没有操作；1：赞；2：踩
								lolNum: 123,
								cryingNum: 10
							},
							commentNum: '22',
							shareNum: '55'
						},
						{
							userPic: '../../static/demo/demo5.jpg',
							userName: '昵称456',
							isAttention: false,
							titleText: '我是标题我是标题我是标题我是',
							isType: 'image',
							titlePic: '../../static/demo/datapic/25.jpg',
							playNumber: '235',
							palyTime: '1822',
							infoNum: {
								userFlag: '1', //0:没有操作；1：赞；2：踩
								lolNum: 123,
								cryingNum: 10
							},
							commentNum: '22',
							shareNum: '55'
						}
					]
				}, {
					list: [{
							userPic: '../../static/demo/demo5.jpg',
							userName: '昵称123',
							isAttention: false,
							titleText: '我是标题我是标题我是标题我是标题我是标题我是标题我是标题',
							isType: 'video',
							titlePic: '../../static/demo/datapic/26.jpg',
							playNumber: '235',
							palyTime: '1822',
							infoNum: {
								userFlag: '1', //0:没有操作；1：赞；2：踩
								lolNum: 123,
								cryingNum: 10
							},
							commentNum: '22',
							shareNum: '55'
						},
						{
							userPic: '../../static/demo/demo6.jpg',
							userName: '昵称456',
							isAttention: false,
							titleText: '我是标题我是标题我是标题我是',
							isType: 'image',
							titlePic: '../../static/demo/datapic/36.jpg',
							playNumber: '235',
							palyTime: '1822',
							infoNum: {
								userFlag: '1', //0:没有操作；1：赞；2：踩
								lolNum: 123,
								cryingNum: 10
							},
							commentNum: '22',
							shareNum: '55'
						},
						{
							userPic: '../../static/demo/demo6.jpg',
							userName: '昵称456',
							isAttention: false,
							titleText: '我是标题我是标题我是标题我是',
							isType: 'image',
							titlePic: '../../static/demo/datapic/35.jpg',
							playNumber: '235',
							palyTime: '1822',
							infoNum: {
								userFlag: '1', //0:没有操作；1：赞；2：踩
								lolNum: 123,
								cryingNum: 10
							},
							commentNum: '22',
							shareNum: '55'
						},
						{
							userPic: '../../static/demo/demo7.jpg',
							userName: '昵称456',
							isAttention: false,
							titleText: '我是标题我是标题我是标题我是',
							isType: 'image',
							titlePic: '../../static/demo/datapic/26.jpg',
							playNumber: '235',
							palyTime: '1822',
							infoNum: {
								userFlag: '1', //0:没有操作；1：赞；2：踩
								lolNum: 123,
								cryingNum: 10
							},
							commentNum: '22',
							shareNum: '55'
						}
					]
				}, {
					list: []
				}, {
					list: []
				}, {
					list: []
				}, {
					list: []
				}],
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					let height = res.windowHeight - uni.upx2px(100)
					this.swiperHeight = height
				}
			});
		},
		methods: {
			changeIndex(index) {
				this.tabIndex = index
			},
			changeTab(e) {
				this.tabIndex = e.detail.current
			}
		}
	}
</script>

<style>


</style>
