<script>
	export default {
		onLaunch() {
			// #ifdef APP-PLUS-NVUE
			const domModule = weex.requireModule('dom')
			domModule.addRule('fontFace',{
				'fontFamily':'iconfont',
				'src':"url('/static/font.ttf')",
			})
			// #endif
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
	@import 'common/free.css';
	@import 'common/common.css';
	/* #ifndef APP-PLUS-NVUE */
	@import './common/free-icon.css';
	/* #endif */
</style>
