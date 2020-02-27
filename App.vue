<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	/* 引入官方css库 */
    /* uni.css - 通用组件、模板样式库，可以当作一套ui库应用 */
    @import './common/uni.css';
	/* 引入图标库 */
	@import url("./common/iconfont.css");
	/* 引入动画库 */
	@import url("./common/animate.css");
	/* 引入公共样式 */
	@import url("./common/common.css");
</style>
