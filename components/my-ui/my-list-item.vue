<template>
	<view class="bg-white flex align-stretch" hover-class="bg-light" @click="$emit('click')">
		<view class="flex align-center justify-between py-2 px-3">
			<slot name="icon"></slot>
			<image v-if="imgUrl" :src="imgUrl" mode="widthFix" style="width: 75rpx;height: 75rpx;">
			</image>
		</view>
		<view :class="isShowBottomLine ? 'border-bottom' : ''" class="flex-1 flex align-center justify-between">
			<text class="font-sm text-dark">{{title}}</text>
			<view class="flex align-center p-2" v-if="isShowRight">
				<slot name="right"></slot>
				<!-- 右箭头 -->
				<text class="iconfont font-md text-light-muted">&#xe60c;</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			imgUrl:{
				type:'String',
				default:''
			},
			title:{
				type:'String',
				default:''
			},
			isShowRight:{
				type:Boolean,
				default:true
			},
			isShowBottomLine:{
				type:Boolean,
				default:true
			}
		},
		data() {
			return {
                
			}
		},
		methods: {

		}
	}
</script>

<style>

</style>