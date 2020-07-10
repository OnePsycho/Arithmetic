<template name="components">
	<view class="page">
		<view class="logo">
			<image src="../../static/logo.png" mode="widthFix" class="logo-image"></image>
			<image src="../../static/myLogo.png" mode="widthFix"></image>
		</view>
		<view class="btn-start">
			<image class="btns-item" src="../../static/btn_start.png" mode="widthFix" @click="onStart"></image>
			<image class="btns-item" src="../../static/btn_rank.png" mode="widthFix" @click="onShowRank"></image>
			<button open-type="share">
				<image src="../../static/btn_share.png" mode="widthFix" @click="onShare"></image>
			</button>
		</view>
		<view class="cu-modal" :class="isShowModal?'show':''" @tap="hideModal">
			<view class="cu-dialog" @tap.stop="">
				<p class="type-title">选择模式</p>
				<view class="type-item" @click="goStart('twoAdd',10)">两位数 / 加法 / 10个</view>
				<view class="type-item" @click="goStart('twoReduce',10)">两位数 / 减法 / 10个</view>
				<view class="type-item" @click="goStart('twoRide',10)">两位数 / 乘法 / 10个</view>
				<view class="type-item" @click="goStart('threeAdd',10)">三位数 / 加法 / 10个</view>
				<p class="type-tips">游戏规则：输入答案点击OK 正确则自动进入下一题 错误则需重新输入正确答案</p>
			</view>
		</view>
	</view>
</template>

<script>
	export default {

		data() {
			return {
				isShowModal: false
			};
		},
		created() {
			// let arr = [...new Set(new Array(80).keys())]
			// let arr2 = []
			// arr.forEach(i => {
			// 	let a = this.getRandom(100,999)
			// 	let b = this.getRandom(100,999)
			// 	arr2.push({
			// 		a:a,
			// 		b:b,
			// 		c:a + b
			// 	})
			// })
			// console.log(JSON.stringify(arr2))
		},
		onShareAppMessage() {
		      return {
		        title: '速算王者-你速算有我厉害吗?',
		        imageUrl: 'https://onepsycho.bj.bcebos.com/bg-share.png',
		        path: '/pages/welcome/home'
		      }
		},
		onShareTimeline(){
			return {
			  title: '速算王者-你速算有我厉害吗?'
			}
		},
		methods: {
			hideModal() {
				this.isShowModal = false
			},

			onShare() {
				
			},

			getRandom(min, max) {
				min = Math.ceil(min);
				max = Math.floor(max);
				return Math.floor(Math.random() * (max - min + 1)) + min;
			},
			onStart() {
				this.isShowModal = true
			},

			onShowRank() {
				alert('即将开放！')
			},

			goStart(type, count) {
				this.isShowModal = false
				uni.showLoading({
					title: '题目马上来'
				})

				setTimeout(() => {
					uni.navigateTo({
						url: '../main/home?type=' + type + '&count=' + count
					})
					uni.hideLoading()
				}, 1000)

			}
		},
		mounted() {},
		destroyed() {}

	}
</script>

<style lang="less">
	.page {
		height: 100vh;
		position: relative;
		padding-bottom: 150rpx;
		font-family: 'myFont';
		font-weight: 200;
		// background: #fff;

		.logo {
			width: 100%;

			image {
				width: 80%;
				margin-left: 10%;
				margin-top: 20px;
			}

			.logo-image {
				width: 34%;
				margin-left: 33%;
				margin-top: 15%;
			}
		}



		.btn-start {
			position: absolute;
			width: 100%;
			bottom: 10%;
			left: 0;

			.btns-item {
				width: 40%;
				margin-left: 30%;
				border: 1px solid #d1d1d1;
				margin-bottom: 30rpx;
			}
			
			button{
				width: 40%;
				margin-left: 30%;
				padding: 0;
				border: none;
				border-radius: 0;
				height: 119rpx;
				background: none;
				
				&::after{
					border: none;
					border-color: #d1d1d1;
					border-bottom: 1px solid #d1d1d1;
					border-radius: 0;
				}
				
				image{
					width: 100%;
					border: 1px solid #d1d1d1;
				}
			}

			&-txt {
				width: 60%;
				margin-left: 20%;
				border: 2px solid #e0e0e0;
				text-align: center;
				height: 150rpx;
				display: flex;
				justify-content: center;
				align-items: center;
				font-size: 32px;
				color: #7a7a7a;
			}
		}
	}

	.type-title {
		margin-top: 50rpx;
		font-size: 22px;

	}

	.cu-dialog {
		padding-bottom: 40rpx;
	}

	.type-item {
		padding: 20rpx 0;
		margin: 40rpx 0;
		font-size: 18px;
		border: 1px solid #e0e0e0;
		box-shadow: 0 0 5px 2px #626262;
		width: 50%;
		margin-left: 25%;
		background: #868686;
		color: #fff;
	}

	.type-tips {
		width: 60%;
		margin-left: 20%;
		color: #888888;
	}
</style>
