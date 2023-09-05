<template>
	<view>
		<!-- 显示时间 -->
		<view v-if="showTime" class="flex justify-center justify-center pb-2 pt-3">
			<text class="font-sm text-light-muted">{{showTime}}</text>
		</view>
		<!-- 气泡 -->
		<view class="px-2 py-1 flex align-start" :class="isSelf ? 'justify-end' : 'justify-start'">
			<!-- 好友 -->
			<template v-if="!isSelf">
				<myAvatar :src="item.avatar" size="70"></myAvatar>
				<text class="iconfont text-white position-absolute icon-left-chat">&#xe609</text>
			</template>
			<view @longpress="onLong" class="rounded ml-3 px-1 list-style" :class="item.user_id === 1 ? 'bg-chat-item mr-3':'bg-white ml-3'" style="max-width: 500rpx;">
				<text class="font-md">{{item.data}}</text>
			</view>
			<!-- 本人 -->
			<template v-if="isSelf">
				<text class="iconfont position-absolute icon-right-chat">&#xe640</text>
				<myAvatar :src="item.avatar" size="70"></myAvatar>
			</template>
		</view>
		<!-- 占位 -->
		<view class="mb-2"></view><strong></strong>
	</view>
</template>

<script>
	import myAvatar from '@/components/my-ui/my-avatar.vue'
	import $T from '@/common/lib/time.js'
	export default {
		components:{
			myAvatar
		},
		props:{
	        item:{
				type:Object,
				default:''
			},
			index:{
				type:Number,
				defaultL:-1
			},
			preTime:{
				type:[String,Number],
				default:0
			}
		},
		computed:{
			isSelf(){
				const id = 1;
				return this.item.user_id === id
			},
			showTime(){
				return $T.getChatTime(this.item.create_time,this.preTime)
			}
		},
		methods: {
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
				this.$emit('long',{x,y,index:this.index})
			}
		}
	}
</script>

<style scoped>
.list-style{
	padding-top: 15rpx;
	padding-bottom: 15rpx;
}
.icon-left-chat{
	left: 98rpx;
	top: 25rpx;
}
.icon-right-chat{
	right: 98rpx;
	top: 25rpx;
	color: #95EC69;
}
.bg-chat-item{
	background-color: #95EC69;
}
</style>
