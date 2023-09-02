<template>
	<view>
		<view :class="getClass">
			<!-- 状态栏 -->
			<view :style="'height:'+statusBarHeight + 'px'"></view>
			<!-- 导航 -->
			<view class="w-100 flex justify-between align-center" style="height: 80rpx;">
				<!-- 左边 -->
				<view class="flex align-center">
					<!-- 返回按钮 -->
					<MyIconButton v-if="isShowBack" @click="back" :icon="'\ue60d'">{{getTitle}}</MyIconButton>
					<!-- 标题 -->
					<slot>
						<text v-if="title" class="font-md ml-3">{{getTitle}}</text>
					</slot>
				</view>
				<!-- 右边 -->
				<view class="flex">
					<slot name="right">
						<my-icon-button :icon="'\ue6e3'"></my-icon-button>
						<my-icon-button @click="openExtend" :icon="'\ue682'"></my-icon-button>
					</slot>
				</view>
			</view>
		</view>
		<!-- 占位 -->
		<view v-if="fixed" :style="fixedStyle"></view>
		<!-- 扩展菜单 -->
		<MyPopUp ref="extend" origin-drop="right top" body-bg-color="bg-dark" :mask-color="false" :body-height="525"
			:body-width="320">
			<view class="flex pt-1 pb-1 flex-column" style="width: 320rpx;height: 525rpx;">
				<view v-for="(item,index) in myExtends" @click="click(item.event)" :key="item.name"
					hover-class="bg-hover-dark" class="flex-1 flex align-center">
					<text class="iconfont font-md text-white pl-3">{{item.icon}}</text>
					<text class="font-md pl-3 text-white">{{item.name}}</text>
				</view>
			</view>
		</MyPopUp>
	</view>
</template>

<script>
	import MyIconButton from '@/components/my-ui/my-icon-button.vue'
	import MyPopUp from './my-pop-up.vue'
	export default {
		components: {
			MyIconButton,
			MyPopUp
		},
		props: {
			title: {
				type: [String, Boolean],
				default: ''
			},
			fixed: {
				type: [Boolean],
				default: true
			},
			noreadnum: {
				type: Number,
				default: 0
			},
			bgColor:{
				type: String,
				default: 'bg-bar'
			},
			isShowBack:{
				type: Boolean,
				default: false
			}
		},
		data() {
			return {
				statusBarHeight: 0,
				navBarHeight: 0,
				myExtends: [{
						name: '发起群聊',
						event: '',
						icon:'\ue633'
					},
					{
						name: '添加好友',
						event: '',
						icon:'\ue65d'
					},
					{
						name: '扫一扫',
						event: '',
						icon:'\ue614'
					},
					{
						name: '首付款',
						event: '',
						icon:'\ue667'
					},
					{
						name: '帮助与反馈',
						event: '',
						icon:'\ue61c'
					}
				],
			}
		},
		methods: {
			openExtend() {
				this.$refs.extend.show(uni.upx2px(415), uni.upx2px(150))
			},
			back(){
				uni.navigateBack()
			}
		},
		computed: {
			fixedStyle() {
				return `height:${this.navBarHeight}px`
			},
			getTitle() {
				return this.noreadnum > 0 ? `${this.title}(${this.noreadnum})` : `${this.title}`;
			},
			getClass(){
				let fixed = this.fixed ? 'fixed-top' : ''
				return `${this.bgColor} ${fixed}`
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