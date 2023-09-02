<template>
	<view @click="$emit('click')" :hover-class="isShowHover ? 'bg-hover-light' : ''" class="flex align-center justify-center" style="width: 70rpx;height: 70rpx;">
		<text class="iconfont font-md">{{icon}}</text>
	</view>
</template>

<script>
	export default {
		props:{
			icon:{
				type:String,
				default:''
			},
			isShowHover:{
				type:Boolean,
				default:false
			}
		}
	}
</script>

<style>
</style>