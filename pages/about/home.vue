<template name="components">
	<view>
		<scroll-view scroll-y class="page">
			<view class="page-header" :style="'top:' + StatusBar + 'px'">
				<view class="cu-bar search">
					<view class="cu-avatar round" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big11010.jpg)"></view>
					<view class="search-form round bg-gray">
						<text class="cuIcon-search"></text>
						<input :adjust-position="false" style="width: 150px;" type="text" placeholder="输入您想搜索的商品" confirm-type="search"></input>
					</view>
				</view>
			</view>
			<image src="../../static/bg.png" class="bg-image" width="100%"></image>
			<BaseSwiper></BaseSwiper>
			<BaseMenu></BaseMenu>
			<view class="title-header">
				<view class="title-text">
					口 / 碑 / 推 / 荐
				</view>
			</view>
			<view class="padding-sm">
				<view class="flex">
					<view class="flex-twice bg-white margin-xs bg-img shadow-blur radius-index solid mimicry" style="border-radius:5px;height:330rpx;background-image:url(https://cdn.nlark.com/yuque/0/2020/jpeg/280373/1584858775313-assets/web-upload/f73df75d-ed8d-49e7-8567-e9ab9f84e055.jpeg)"></view>
					<view class="flex-sub radius margin-right-xs margin-left-sm">
						<view class="flex-sub bg-white margin-top-xs bg-img shadow-blur radius-index solid mimicry" style="border-radius:5px;height:150rpx;background-image:url(https://cdn.nlark.com/yuque/0/2020/jpeg/280373/1584858674362-assets/web-upload/f81ba224-020e-4bac-8117-fcdd65b7835e.jpeg)"></view>
						<view class="flex-sub bg-white margin-top bg-img shadow-blur radius-index solid mimicry" style="border-radius:5px;height:150rpx;background-image:url(https://cdn.nlark.com/yuque/0/2020/jpeg/280373/1584858674225-assets/web-upload/5bda67fb-3f5e-47c3-89fd-96dd98b7d2e7.jpeg)"></view>
					</view>
				</view>
			</view>
			<view class="title-header">
				<view class="title-text">
					特 / 价 / 清 / 货
				</view>
			</view>
			<view class="cu-card">
				<image src="https://cdn.nlark.com/yuque/0/2020/jpeg/280373/1584783211826-assets/web-upload/2dbdc8ed-a4d7-463c-9dbb-ce9b6487157b.jpeg"
				 mode="widthFix"></image>
				<image src="https://cdn.nlark.com/yuque/0/2020/jpeg/280373/1584780088958-assets/web-upload/b2381013-3d6e-4405-babb-2d252721d5b0.jpeg"
				 mode="widthFix"></image>
				<image src="https://cdn.nlark.com/yuque/0/2020/jpeg/280373/1584780089083-assets/web-upload/426204ff-42c6-4008-99ee-313145208138.jpeg"
				 mode="widthFix"></image>
				<image src="https://cdn.nlark.com/yuque/0/2020/jpeg/280373/1584780088348-assets/web-upload/a6a53211-17b2-4643-987d-2da0de81437a.jpeg"
				 mode="widthFix"></image>
			</view>
			<view class="title-header">
				<view class="title-text">
					爆 / 款 / 靓 / 品
				</view>
			</view>
			<view class="padding-sm padding-bottom-index">
				<view class="margin-top">
					<view class="products-box">
						<view class="basis-df padding-xs" v-for="(item,index) in product" :key="index">
							<view class="grid col-1 grid-square flex-sub">
								<image :src="item.url" mode="widthFix"></image>
							</view>
							<view class="grid col-1 margin-bottom">
								<view class="">
									<view class="text-xl product-title tn-align">
										<text class="text-black index-title text-df name-title-a">{{item.title}}</text>
									</view>
									<view class="text-xl product-price">
										<text class="text-red">￥{{item.price}}</text>
										<text class="delete-price text-sm text-gray">￥{{item.priceno}}</text>
									</view>
								</view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	import BaseMenu from '@/components/BaseMenu.vue'
	import BaseSwiper from '@/components/BaseSwiper.vue'
	export default {
		components: {
			BaseMenu,
			BaseSwiper
		},
		data() {
			return {
				StatusBar: this.StatusBar - 2,
				product: [{
					title: "便捷充电式榨汁机 青色款",
					price: "199",
					priceno: "219",
					url: "https://cdn.nlark.com/yuque/0/2020/jpeg/280373/1584774092172-assets/web-upload/67536cb8-7210-4ae2-8e2a-b441ea9d98fa.jpeg"
				}, {
					title: "便捷充电式榨汁机 粉色款",
					price: "199",
					priceno: "219",
					url: "https://cdn.nlark.com/yuque/0/2020/jpeg/280373/1584774092268-assets/web-upload/163bb891-c335-4fdb-bb91-a84c2f85882a.jpeg"
				}, {
					title: "家用冰箱 简约设计",
					price: "9999",
					priceno: "10499",
					url: "https://cdn.nlark.com/yuque/0/2020/jpeg/280373/1584774091511-assets/web-upload/47b32f22-e958-4e3c-bd37-1230c483514e.jpeg"
				}, {
					title: "洗碗机 高效除菌",
					price: "1999",
					priceno: "2299",
					url: "https://cdn.nlark.com/yuque/0/2020/jpeg/280373/1584774092053-assets/web-upload/f3046148-1791-4ef0-ad1e-e714051de8f5.jpeg"
				}],
			};
		},
		onLoad() {
			this.TowerSwiper('swiperList');
			// 初始化towerSwiper 传已有的数组名即可
		},
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

		.title-header {
			display: -webkit-flex;
			display: flex;
			height: 120rpx;
			font-size: 40rpx;
			-webkit-align-items: center;
			align-items: center;
			-webkit-justify-content: center;
			justify-content: center;
			font-weight: bold;
			background-image: url(https://cdn.nlark.com/yuque/0/2019/png/280373/1570758062258-assets/web-upload/1274f32f-78f4-409c-b7be-b70da5e379d8.png);
			background-size: cover;

			.title-text {
				background-image: -webkit-linear-gradient(0deg, #ff8a34, #FBBD12);
				-webkit-background-clip: text;
				-webkit-text-fill-color: transparent;
			}
		}
		
		.products-box{
			display: flex;
			flex-wrap: wrap;
			
			.padding-xs{
				width: 50%;
			}
		}

		.cu-card image {
			width: 90%;
			margin-left: 5%;
			margin-top: 20rpx;
			border-radius: 5px;
		}



	}

	.bg-image {
		width: 100% !important;
	}
</style>
