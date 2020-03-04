<template>
	<view>
		<index-tab-bar :tabBars="tabBars" :tabIndex="tabIndex" @changeIndex="changeIndex"></index-tab-bar>
		<!-- :style="{height:swiperHeight+'px'}" -->
		<view class="uni-tab-bar">
			<!-- 顶部导航 -->
			<swiper class="swiper" :current="tabIndex" @change="changeTab" :style="{height:swiperHeight+'px'}">
				<swiper-item class="swiper-item" v-for="(item,index) in newList" :key="index">
					<scroll-view scroll-y class="list " @scrolltolower="loaderMore(index)">
						<template v-if="item.list.length > 0">
							<!-- 图文列表 -->
							<view class="list-cell" v-for="(listItem,listIndex) in item.list" :key="listIndex">
								<index-list :item="listItem" :index="listIndex"></index-list>
							</view>
							<!-- 上拉加载 -->
							<load-more :loaderText="item.loaderMore"></load-more>
						</template>
						<template v-else>
							<nothing-info></nothing-info>
						</template>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import indexTabBar from '../../components/index/index-tabBar.vue'
	import indexList from '../../components/index/index-list.vue'
	import loadMore from '../../components/common/loadMore.vue'
	import NothingInfo from '../../components/common/nothing.vue'
	export default {
		components: {
			indexList,
			indexTabBar,
			loadMore,
			NothingInfo
		},
		data() {
			return {
				swiperHeight: 0, //默认高度
				tabIndex: 1, //默认第一个
				tabBars: [{ //顶部栏数据
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
				newList: [{ //每一个tabbar的数据
					loaderMore: '上拉加载更多...',
					list: [{
							userPic: '../../static/demo/demo5.jpg', //用户头像
							userName: '昵称123', //用户昵称
							isAttention: false, //是否关注
							titleText: '我是标题我是标题我是标题我是标题我是标题我是标题我是标题', //标题
							isType: 'video', //内容类型图文和视频两种
							titlePic: '../../static/demo/datapic/28.jpg', //内容背景图
							playNumber: '235', //播放数量
							palyTime: '1822', //播放时长毫秒
							infoNum: { //用户操作
								userFlag: '0', //0:没有操作；1：赞；2：踩
								lolNum: 123, //笑脸点赞
								cryingNum: 10 //哭脸踩
							},
							commentNum: '22', //评论数
							shareNum: '55', //分享数量
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
								userFlag: '0', //0:没有操作；1：赞；2：踩
								lolNum: 123,
								cryingNum: 10
							},
							commentNum: '22',
							shareNum: '55'
						}
					]
				}, {
					loaderMore: '上拉加载更多...',
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
								userFlag: '0', //0:没有操作；1：赞；2：踩
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
								userFlag: '0', //0:没有操作；1：赞；2：踩
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
								userFlag: '0', //0:没有操作；1：赞；2：踩
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
					loaderMore: '上拉加载更多...',
					list: []
				}, {
					loaderMore: '上拉加载更多...',
					list: []
				}, {
					loaderMore: '上拉加载更多...',
					list: []
				}, {
					loaderMore: '上拉加载更多...',
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
		onNavigationBarSearchInputClicked() {
				uni.navigateTo({
					url:"../search/search"
				})
		},
		methods: {
			// 上拉加载
			loaderMore(index) {
				if (this.newList[index].loaderMore != '上拉加载更多...') {
					return;
				}
				this.newList[index].loaderMore = '加载中...'
				setTimeout(() => {
					let obj = {
						userPic: '../../static/demo/demo5.jpg', //用户头像
						userName: '昵称123', //用户昵称
						isAttention: false, //是否关注
						titleText: '我是标题我是标题我是标题我是标题我是标题我是标题我是标题', //标题
						isType: 'video', //内容类型图文和视频两种
						titlePic: '../../static/demo/datapic/28.jpg', //内容背景图
						playNumber: '235', //播放数量
						palyTime: '1822', //播放时长毫秒
						infoNum: { //用户操作
							userFlag: '1', //0:没有操作；1：赞；2：踩
							lolNum: 123, //笑脸点赞
							cryingNum: 10 //哭脸踩
						},
						commentNum: '22', //评论数
						shareNum: '55', //分享数量
					}
					this.newList[index].list.push(obj)
					this.newList[index].loaderMore = '上拉加载更多...'
				}, 200)
				// this.newList[index].loaderMore = '没有更多了'
			},
			// 切换导航栏
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
