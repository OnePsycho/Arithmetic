<template name="components">
	<view class="page">
		<!-- 头部 -->
		<view class="calc-header">
			<navigator url="../welcome/home" open-type="navigateBack">
				<image src="../../static/close.png" mode="widthFix"></image>
			</navigator>
			<view class="calc-header-right">
				<span>{{minStr}}</span>
				<span>:</span>
				<span>{{secStr}}</span>
				<span>:</span>
				<span>{{msStr}}</span>
			</view>
			<view class="progress" :style="'width:' + curProgress + '%'"></view>
		</view>
		<!-- 内容部分 -->
		<view class="calc-content">
			<view class="calc-content-question">
				<span>{{ numA }}</span>
				<span> {{ type === 'twoAdd' || type === 'threeAdd' ? '+' : type === 'twoReduce' ? '-' : 'x' }} </span>
				<span>{{ numB }}</span>
			</view>
			<view class="calc-content-answer">
				<input type="text" :value="curAnswer"  disabled/>
			</view>
		</view>
		<!-- 计算部分 -->
		<view class="calc-box">
			<view class="calc-box-item" v-for="(item,index) in numsList" :key="index" @click="onItemClick(item + 1)">
				{{ index + 1 }}
			</view>
			<view class="calc-box-item" @click="onItemClick('cancel')">C</view>
			<view class="calc-box-item" @click="onItemClick(0)">0</view>
			<view class="calc-box-item" @click="onItemClick('OK')">OK</view>
		</view>
		
		<view class="cu-modal" :class="isShowModal ?'show':''">
			<view class="cu-dialog">
				<view class="cu-bar bg-white justify-end">
					<view class="content">答题完成</view>
					<view class="action" @tap="hideModal">
						<text class="cuIcon-close text-red"></text>
					</view>
				</view>
				<view class="padding-xl">
					{{ '答题完成！最终用时: ' + minStr + ':' + secStr + ':' + msStr  }}
				</view>
				<view class="cu-bar bg-white">
					<view class="action margin-0 flex-sub text-green solid-left" @tap="hideModal">取消</view>
					<view class="action margin-0 flex-sub  solid-left" @tap="onConfirm">重新挑战</view>
					<view class="action margin-0 flex-sub  solid-left">
						<button open-type="share">分享给好友</button>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import listTwoReduce from '../../utils/list-two-reduce.js'
	import listTwoAdd from '../../utils/list-two-add.js'
	import listTwoRide from '../../utils/list-two-ride.js'
	import listThreeAdd from '../../utils/list-three-add.js'
	export default {

		data() {
			return {
				numsList:[0,1,2,3,4,5,6,7,8],
				curAnswer:'',
				curIndex:0,
				curProgress:0,
				numA:null,
				numB:null,
				count:10,
				nums:null,
				type:null,
				min:0,
				minStr:'',
				second:0,
				secStr:'',
				ms:0,
				msStr:'',
				timer:null,
				isShowModal:false,
				questionList:[]
			};
		},
		onLoad(options) {
			if(options) {
				this.type = options.type
				this.count = options.count
				this.init()
			}
		},
		created(options) {
			if(options) {
				this.type = options.type
				this.count = options.count
				this.init()
			}
		},
		onShareAppMessage(res) {
			if (res.from === 'button') {
			    let typeStr = this.type === 'twoAdd' ? '两位数加法' : this.type === 'twoReduce' ? '两位数减法' : this.type === 'twoRide' ? '两位数乘法' : '三位数加法'
			      return {
			        title: this.count + '道' + typeStr  + '速算我只用了 ' + this.minStr + ':' + this.secStr + ':' + this.msStr + ' 就完成了，你呢？',
			        imageUrl: 'https://onepsycho.bj.bcebos.com/bg-share.png',
			        path: '/pages/welcome/home'
			      }
			  } else if (res.from === 'menu'){
				   return {
					 title: '速算王者-你速算有我厉害吗?',
					 imageUrl: 'https://onepsycho.bj.bcebos.com/bg-share.png',
					 path: '/pages/welcome/home'
				   }
			  }
			
		},
		onShareTimeline(){
			
		},
		methods: {
			init(){
				let list = this.type === 'twoAdd' ? listTwoAdd : this.type === 'twoReduce' ? listTwoReduce : this.type === 'twoRide' ? listTwoRide : listThreeAdd
				this.questionList = this.getRandomArrayElements(list.default,this.count)
				this.numA = this.questionList[0].a
				this.numB = this.questionList[0].b
				clearInterval(this.timer)
				this.timer = setInterval(this.show,10)
			},
			
			hideModal(){
				this.isShowModal = false
			},
			
			onConfirm(){
				uni.reLaunch({
				    url: '/pages/welcome/home'
				});
			},
			
			show(){
				var min= this.min;
				var sec= this.second;
				var ms= this.ms;
				
				ms++;
				if(sec==60){
					min++;sec=0;
				}
				if(ms==100){
					sec++;ms=0;
				}
				var msStr=ms;
				if(ms<10){
					msStr="0"+ms;
				}
				var secStr=sec;
				if(sec<10){
					secStr="0"+sec;
				}
				var minStr=min;
				if(min<10){
					minStr="0"+min;
				}
				this.minStr = minStr
				this.secStr = secStr
				this.msStr = msStr
				
				this.min = min
				this.second = sec
				this.ms = ms
			},
			
			onItemClick(val){
				if(val === 'cancel'){
					this.curAnswer = ''
				}else if(val === 'OK'){
					if(this.curIndex < this.count - 1){
						if(+this.curAnswer === this.questionList[this.curIndex].c){
							this.curProgress = (this.curIndex + 1) / this.count * 100
							this.curIndex += 1
							this.numA = this.questionList[this.curIndex].a
							this.numB = this.questionList[this.curIndex].b
							this.curAnswer = ''
						}else{
							this.curAnswer = ''
						}
						
					}else{
						clearInterval(this.timer)
						this.isShowModal = true
					}
					
				}else{
					this.curAnswer = this.curAnswer + val
				}
			},
			
			getRandomArrayElements(arr, count) {
			    var shuffled = arr.slice(0), i = arr.length, min = i - count, temp, index;
			    while (i-- > min) {
			        index = Math.floor((i + 1) * Math.random());
			        temp = shuffled[index];
			        shuffled[index] = shuffled[i];
			        shuffled[i] = temp;
			    }
			    return shuffled.slice(min);
			}
		},
		destroyed() {
			clearInterval(this.timer)
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

		.calc-header{
			position: relative;
			width: 100%;
			height: 60px;
			padding: 18px;
			display: flex;
			justify-content: space-between;
			align-items: center;
			border-bottom: 1px solid #e0e0e0;
			
			&-right{
				font-size: 28px;
			}
			
			.progress{
				position: absolute;
				left: 0;
				bottom: -3px;
				height: 3px;
				width: 100%;
				background: #333333;
				
			}
			
			image{
				width: 20px;
			}
		}
		
		.calc-content{
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			margin-top: 100rpx;
			color:#585858;
			
			&-question{
				font-size: 40px;
				
				span{
					margin: 0 20rpx;
				}
			}
			
			&-answer{
				margin-top: 60rpx;
				
				input{
					background: #e6e6e6;
					width: 60%;
					margin-left: 20%;
					height: 140rpx;
					line-height: 100rpx;
					font-size: 42px;
					padding: 10rpx;
					color:#000;
					text-align: center;
					letter-spacing: 1px;
				}
			}
		}
		
		.calc-box{
			position: absolute;
			width:100%;
			bottom: 0;
			left: 0;
			display: flex;
			flex-wrap: wrap;
			
			&-item{
				flex: 1 1 33.33%;
				height: 180rpx;
				display: flex;
				justify-content: center;
				align-items: center;
				font-size: 30px;
				color:#585858;
				border: .5px solid #e0e0e0;
				margin: -.5px;
			}
		}
		
		.cu-bar{
			button{
				padding: 0;
				border: none;
				border-radius: 0;
				height: 19px;
				font-size: 14px;
				color:#666;
				background: none;
				font-family: 'myFont';
				line-height: normal;
				
				&::after{
					border: none;
					border-color: #d1d1d1;
					border-radius: 0;
				}
			}
		}
	}
</style>
