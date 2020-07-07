<template name="components">
	<view class="page">
		<view class="btn-start">
			<navigator url="../main/home">
				<view class="btn-start-txt">
					开始挑战
				</view>
			</navigator>
			
		</view>
	</view>
</template>

<script>
	export default {

		data() {
			return {
				
			};
		},
		created() {
			
		},
		methods: {
			
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
		
		.btn-start{
			position: absolute;
			width: 100%;
			bottom: 10%;
			left: 0;
			
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
</style>
