<template name="components">
	<view class="page">
		<view class="logo">
			<image src="../../static/logo.png" mode="widthFix" class="logo-image"></image>
			<image src="../../static/myLogo.png" mode="widthFix"></image>
		</view>
		<view class="btn-start">
				<image src="../../static/btn_share.png" mode="widthFix"></image>
				<image src="../../static/btn_rank.png" mode="widthFix"></image>
				<image src="../../static/btn_start.png" mode="widthFix" @click="onStart"></image>
		</view>
		<view class="cu-modal" :class="isShowModal?'show':''" @tap="hideModal">
			<view class="cu-dialog" @tap.stop="">
				<p class="type-title">选择模式</p>
				<view class="type-item">两位数 / 乘法 / 10个</view>
				<view class="type-item">两位数 / 乘法 / 10个</view>
				<view class="type-item">两位数 / 乘法 / 10个</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {

		data() {
			return {
				isShowModal:true
			};
		},
		created() {
			
		},
		methods: {
			hideModal(){
				this.isShowModal = false
			},
			onStart(){
				this.isShowModal = true
			}
		},
		mounted() {
		},
		destroyed() {
		}
		
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
		
		.logo{
			width: 100%;
			
			image{
				width: 80%;
				margin-left: 10%;
				margin-top: 20px;
			}
			
			.logo-image{
				width: 40%;
				margin-left: 30%;
				margin-top: 20%;
			}
		} 
		
		
		
		.btn-start{
			position: absolute;
			width: 100%;
			bottom: 10%;
			left: 0;
			
			image{
				width: 40%;
				margin-left: 30%;
				border: 1px solid #d1d1d1;
				margin-bottom: 30rpx;
			}
			
			&-txt{
				width: 60%;
				margin-left: 20%;
				border: 2px solid #e0e0e0;
				text-align: center;
				height: 150rpx;
				display: flex;
				justify-content: center;
				align-items: center;
				font-size: 32px;
				color:#7a7a7a;
			}
		}
	}
	.type-title{
		margin-top: 50rpx;
		font-size: 22px;
		
	}
	
	.type-item{
		padding: 40rpx 0;
		margin: 60rpx 0;
		font-size: 18px;
		border: 1px solid #e0e0e0;
		width: 60%;
		margin-left: 20%;
		background: #989898;
		color: #fff;
	}
</style>
