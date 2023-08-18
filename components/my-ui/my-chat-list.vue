<template>
	<view class="flex align-center" hover-class="bg-hover-light" @click="onClick(item)" @longpress="onLong">
		<view class="flex align-center justify-center position-relative" style="width: 145rpx;height: 135rpx;">
			<MyAvatar :src="item.avatar"></MyAvatar>
			<MyBadge v-if="item.num > 0" badgeClass="position-absolute" badgeStyle="top: 10rpx;right: 10rpx;" :num="item.num"></MyBadge>
		</view>
		<view class="flex flex-column flex-1 pr-1 border-bottom py-2 border-light-secondary">
			<view class="flex justify-between">
				<text>{{item.nickname}}</text>
				<text class="font-sm text-light-muted">{{item.update_time | formatTime}}</text>
			</view>
			<text class="text-ellipsis text-light-muted font-sm mt-2">{{item.data}}</text>
		</view>
	</view>
</template>

<script>
	import $Time from '@/common/lib/time.js'
	import MyAvatar from '@/components/my-ui/my-avatar.vue'
	import MyBadge from '@/components/my-ui/my-badge.vue'
	import mixin from '@/common/mixin/base.js'
	export default {
		props: {
			item: Object,
		},
		mixins:[mixin],
		components: {
			MyAvatar,
			MyBadge
		},
		data() {
			return {

			}
		},
		filters: {
			formatTime(value) {
				return $Time.gettime(value)
			}
		},
		methods:{
			onClick(item){
				this.$emit('click',item)
			},
			onLong(e){
				let x = 0
				let y = 0
				// #ifdef APP-PLUS-NVUE
				if(Array.isArray(e.changedTouches) && e.changedTouches.length > 0){
					x = e.changedTouches[0].screenX
					y = e.changedTouches[0].screenY
				}
				// #endif
				// #ifdef MP
				x = e.detail.x
				y = e.detail.y
				// #endif
				this.$emit('long',{x,y})
			}
		}
	}
</script>

<style>

</style>