<template>
	<view>
		<image :class="type" :src="src" mode="aspectFill" :style="getStyle"/>
	</view>
</template>

<script>
	export default {
		props:{
			src:{
				type:String,
				default:''
			},
			type:{
				type:String,
				default:'rounded'
			},
			size:{
				type:[String,Number],
				default:95
			}
		},
		computed:{
			getStyle(){
				return `width:${this.size}rpx;height:${this.size}rpx`
			}
		}
	}
</script>

<style>

</style>
