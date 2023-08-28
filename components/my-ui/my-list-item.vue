<template>
	<view class="bg-white flex align-stretch" hover-class="bg-light" @click="$emit('click')">
		<view class="flex align-center justify-between py-2 px-3">
			<image v-if="imgUrl" :src="imgUrl" mode="widthFix" style="width: 75rpx;height: 75rpx;">
			</image>
		</view>
		<view class="flex-1 border-bottom flex align-center">
			<text class="font-sm text-dark">{{title}}</text>
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