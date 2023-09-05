<template>
	<div class="" style="z-index: 9999;overflow: hidden;" v-if="status">
		<!-- 蒙版 -->
		<div v-if="mask" @click="hide" class="position-fixed top-0 right-0 left-0 bottom-0" :style="getMaskColor"></div>
		<!-- 弹出框内容 -->
		<div ref="mypop" class="position-fixed my-animation triangle" :style="getBodyStyle" :class="getBodyClass">
			<slot></slot>
		</div>
	</div>
</template>

<script>
	// #ifdef APP-PLUS-NVUE
	const animation = weex.requireModule('animation')
	// #endif
	export default {
		props: {
			//蒙版颜色
			maskColor: {
				type: Boolean,
				default: false
			},
			//是否需要蒙版
			mask: {
				type: Boolean,
				default: true
			},
			//是否处于底部
			fixBottom: {
				type: Boolean,
				default: false
			},
			//弹出层高度
			bodyHeight: {
				type: Number,
				default: 0
			},
			//弹出层宽度
			bodyWidth: {
				type: Number,
				default: 0
			},
			//背景颜色
			bodyBgColor: {
				type: String,
				default: 'bg-white'
			},
			//变形原点
			originDrop: {
				type: String,
				default:'top left'
			},
			tabbarHeight:{
				type:Number,
				default:0
			}
		},
		data() {
			return {
				status: false,
				x: -1,
				y: -1,
				maxX: 0,
				maxY: 0
			}
		},
		computed: {
			getMaskColor() {
				let color = this.maskColor ? 0.5 : 0
				return `backgroundColor:rgba(0,0,0,${color})`
			},
			getBodyClass() {
				let fixBottom = this.fixBottom ? 'left-0 right-0 bottom-0' : 'rounded border'
				return `${this.bodyBgColor} ${fixBottom}`
			},
			getBodyStyle() {
				let left = this.x > -1 ? `left:${this.x}px;` : ''
				let top = this.y > -1 ? `top:${this.y}px;` : ''
				return `${left};${top}`
			},
		},
		methods: {
			show(x = -1, y = -1) {
				this.x = x > this.maxX ? this.maxX - 20 : x
				this.y = y > this.maxY ? this.maxY - 20 : y
				this.status = true
				//动画
				// #ifdef APP-PLUS-NVUE
				this.$nextTick(() => {
					animation.transition(this.$refs.mypop, {
						styles: {
							transform: 'scale(1,1)',
							transformOrigin: this.originDrop,
							opacity: 1,
						},
						duration: 200, //ms
						timingFunction: 'ease',
						needLayout: false,
						delay: 0 //ms
					}, function() {

					})
				})
				// #endif 
			},
			hide() {
				// #ifdef APP-PLUS-NVUE
				animation.transition(this.$refs.mypop, {
					styles: {
						transform: 'scale(0,0)',
						transformOrigin: this.originDrop,
						opacity: 0,
					},
					duration: 200, //ms
					timingFunction: 'ease',
					needLayout: false,
					delay: 0 //ms
				}, () => {
					this.status = false
				})
				// #endif 
				// #ifndef APP-PLUS-NVUE
				this.status = false
				// #endif
			},
		},
		mounted() {
			const res = uni.getSystemInfoSync()
			this.maxY = res.windowHeight - uni.upx2px(this.bodyHeight) - uni.upx2px(this.tabbarHeight)
			this.maxX = res.windowWidth - uni.upx2px(this.bodyWidth)
		}
	}
</script>

<style scoped>
	.my-animation {
		/* #ifdef APP-PLUS-NVUE */
		transform: scale(0, 0);
		opacity: 0;
		/* #endif */
	}
</style>