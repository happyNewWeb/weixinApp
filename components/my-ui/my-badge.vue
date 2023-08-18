<template>
	<text class="my-badge bg-danger text-white rounded-circle" 
		:class="badgeClass" 
		:style="badgeStyle">{{num > 99 ? '99+' : num}}</text>
</template>

<script>
	export default {
		props: {
			badgeClass: {
				type: String,
				default: ""
			},
			badgeStyle: {
				type: String,
				default: ""
			},
			num:{
				type:[String,Number],
				default:'',
			}
		},
	}
</script>

<style scoped>
	.my-badge {
		padding: 0 8rpx 0 8rpx;
		font-size: 25rpx;
	}
</style>