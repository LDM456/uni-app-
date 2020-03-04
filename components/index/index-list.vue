<template>
	<view class="list-cell animated bounceIn">
		<view class="cell_list_c cell_list_between cell-top">
			<view>
				<image :src="item.userPic" mode="widthFix" lazy-load></image>
				<text>{{item.userName}}</text>
			</view>
			<view class="cell_list_c cell_list_center attention_btn">
				<view class="cell_list_c cell_list_center" v-show="!item.isAttention" @tap="setAttention(index)">
					<view class="icon iconfont icon-zengjia"></view>关注
				</view>
				<view class="icon iconfont icon-guanbi"></view>
			</view>
		</view>
		<view class="cell-text" @tap="goToDetail()">{{item.titleText}}</view>
		<view class="cell_list_c cell_list_center cell-imgage" @tap="goToDetail()">
			<image :src="item.titlePic" mode="widthFix" lazy-load></image>
			<view class="icon iconfont icon-bofang cell_play"></view>
			<view class="cell_list_c cell_play_num">
				{{item.playNumber}}次播放 {{item.palyTime}}
			</view>
		</view>
		<view class="cell_list_c cell_list_between cell-bottom">
			<view class="cell_list_c lolStyle">
				<view :class="{active:item.infoNum.userFlag == 1}" @tap="clickTap('lol')">
					<view class="icon iconfont icon-icon_xiaolian-mian"></view>
					{{item.infoNum.lolNum}}
				</view>
				<view :class="{active:item.infoNum.userFlag == 2}" @tap="clickTap('cry')">
					<view class="icon iconfont icon-kulian"></view>
					{{item.infoNum.cryingNum}}
				</view>
			</view>
			<view class="cell_list_c">
				<view>
					<view class="icon iconfont icon-pinglun1"></view>
					{{item.commentNum}}
				</view>
				<view>
					<view class="icon iconfont icon-zhuanfa"></view>
					{{item.shareNum}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		},
		methods: {
			// 点击关注
			setAttention(index) {
				this.item.isAttention = true;
				uni.showToast({
					title: '关注成功',
					position: 'center',
					duration: 2000
				})
			},
			// 点击笑脸和哭脸的切换
			clickTap(type) {
				switch (type) {
					case 'lol':
						if (this.item.infoNum.userFlag == 1) {
							return
						};
						this.item.infoNum.lolNum++;
						if (this.item.infoNum.userFlag == 2) {
							this.item.infoNum.cryingNum--
						}
						this.item.infoNum.userFlag = 1
						break;
					case 'cry':
						if (this.item.infoNum.userFlag == 2) {
							return
						};
						this.item.infoNum.cryingNum++;
						if (this.item.infoNum.userFlag == 1) {
							this.item.infoNum.lolNum--;
						}
						this.item.infoNum.userFlag = 2
						break;
				}
			},
			// 进入详情页
			goToDetail() {
				console.log('进入详情页')
			}
		}
	}
</script>

<style>
	.list-cell {
		padding: 20upx;
		border-bottom: 1upx solid #eeeeee;
	}

	.cell-top,
	.cell-bottom {
		color: #9e9e9e;
	}

	.cell-top image {
		width: 88upx;
		height: 88upx;
		border-radius: 50%;
		vertical-align: middle;
		margin-right: 20upx;
	}

	.attention_btn>view:nth-child(1) {
		border-radius: 5px;
		width: 110upx;
		height: 46upx;
		font-size: 28upx;
		background: #f4f4f4;
		color: #000;
		margin-right: 20upx;
	}

	.attention_btn>view:nth-child(1) view {
		font-size: 24upx;
		margin-right: 10upx;
		vertical-align: middle;
		font-weight: 600;
	}

	.cell-text {
		font-size: 32upx;
		line-height: 40upx;
		color: #000000;
		margin: 15upx 0 30upx 0;
	}

	.cell-imgage {
		position: relative;
	}

	.cell-imgage image {
		width: 100%;
		border-radius: 20upx;
	}

	.cell_play {
		position: absolute;
		font-size: 140upx;
		color: #FFFFFF;
	}

	.cell_play_num {
		position: absolute;
		right: 15upx;
		bottom: 10upx;
		padding: 1upx 14upx;
		font-size: 22upx;
		border-radius: 40upx;
		background: rgba(51, 51, 51, 0.7);
		color: #FFFFFF;
	}

	.cell-bottom {
		margin: 28upx 0;
	}

	.cell-bottom view {
		display: inline-block;
		margin: 0 10upx;
		font-size: 28upx;
		vertical-align: bottom;
	}

	.lolStyle {
		color: #9E9E9E;
	}

	.lolStyle .active,
	.lolStyle .active>view {
		color: #fede33;
	}
</style>
