<template name="components">
	<view>
		<scroll-view scroll-y class="page">
			<cu-custom bgColor="bg-gradual-blue"><block slot="content">全部商品</block></cu-custom>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				StatusBar: this.StatusBar - 2,

			};
		},
		onLoad() {},
		created() {},
		methods: {

		}
	}
</script>

<style lang="less">
	.page {
		height: 100vh;
		padding-bottom: 150rpx;
		background: #fff;

		.page-header {
			position: absolute;
			top: 4%;
			left: 0;
			z-index: 999;
			width: 70%;
		}

		.cu-bar .search-form {
			height: 56rpx;
			line-height: 40rpx;
		}
	}
</style>
