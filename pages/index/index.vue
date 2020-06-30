<template>
	<view>
		<BaseMain v-if="PageCur=='home'"></BaseMain>
		<BaseMall v-if="PageCur=='mall'"></BaseMall>
		<BaseOrder v-if="PageCur=='order'"></BaseOrder>
		<BaseAbout v-if="PageCur=='my'"></BaseAbout>
		<view class="cu-bar tabbar bg-white shadow foot">
			<view class="action" @click="NavChange" data-cur="home">
				<view class='cuIcon-cu-image'>
					<image :src="'/static/tabbar/home' + [PageCur=='home'?'_cur':''] + '.png'"></image>
				</view>
				<view :class="PageCur=='home'?'text-blue':'text-gray'">首页</view>
			</view>
			<view class="action" @click="NavChange" data-cur="mall">
				<view class='cuIcon-cu-image'>
					<image :src="'/static/tabbar/mall' + [PageCur == 'mall'?'_cur':''] + '.png'"></image>
				</view>
				<view :class="PageCur=='mall'?'text-blue':'text-gray'">商城</view>
			</view>
			<view class="action" @click="NavChange" data-cur="order">
				<view class='cuIcon-cu-image'>
					<image :src="'/static/tabbar/order' + [PageCur == 'order'?'_cur':''] + '.png'"></image>
				</view>
				<view :class="PageCur=='order'?'text-blue':'text-gray'">订单</view>
			</view>
			<view class="action" @click="NavChange" data-cur="my">
				<view class='cuIcon-cu-image'>
					<image :src="'/static/tabbar/my' + [PageCur == 'my'?'_cur':''] + '.png'"></image>
				</view>
				<view :class="PageCur=='my'?'text-blue':'text-gray'">我的</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				PageCur: 'home'
			}
		},
		methods: {
			NavChange: function(e) {
				this.PageCur = e.currentTarget.dataset.cur
			}
		}
	}
</script>

<style>

</style>
