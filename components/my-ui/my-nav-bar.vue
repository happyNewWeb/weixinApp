<template>
	<view>
		<view class="bg-bar" :class="fixed?'fixed-top':''">
			<!-- 状态栏 -->
			<view :style="'height:'+statusBarHeight + 'px'"></view>
			<!-- 导航 -->
			<view class="w-100 flex justify-between align-center" style="height: 80rpx;">
				<!-- 左边 -->
				<view class="">
					<!-- 标题 -->
					<slot>
						<text v-if="title" class="font-md ml-3">{{getTitle}}</text>
					</slot>
				</view>
				<!-- 右边 -->
				<view class="flex">
					<my-icon-button :icon="'\ue6e3'" @xxx="ccc"></my-icon-button>
					<my-icon-button @click="$emit('search')" :icon="'\ue682'"></my-icon-button>
				</view>
			</view>
		</view>
		<!-- 占位 -->
		<view v-if="fixed" :style="fixedStyle"></view>
	</view>
</template>

<script>
	import MyIconButton from '@/components/my-ui/my-icon-button.vue'
	export default {
		components: {
			MyIconButton
		},
		props: {
			title: {
				type: [String, Boolean],
				default: ''
			},
			fixed:{
				type: [Boolean],
				default: true
			},
			noreadnum:{
				type:Number,
				default:0
			}
		},
		data() {
			return {
				statusBarHeight: 0,
				navBarHeight: 0
			}
		},
		methods: {

		},
		computed: {
			fixedStyle() {
				return `height:${this.navBarHeight}px`
			},
			getTitle(){
				return this.noreadnum > 0 ? `${this.title}(${this.noreadnum})` : `${this.title}`; 
			}
		},
		mounted() {
			//#ifdef APP-PLUS-NVUE
			this.statusBarHeight = plus.navigator.getStatusbarHeight()
			//#endif
			this.navBarHeight = this.statusBarHeight + uni.upx2px(80)
		}
	}
</script>

<style>

</style>