<template>
	<view>
		<view class="title">
			今日文案
		</view>
		<view class="text">
			{{msg}}
		</view>
		<button type="primary" @click="next" class="button1">查看下一个</button>
		<view class="text">
			{{msg1}}
		</view>
		<view class="from">来源：{{msgfrom}}</view>
		<view class="from">作者：{{msgcreator}}</view>
		<button type="primary" @click="next1" class="button1">查看下一个</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				msg:"",
				msg1:"",
				msgfrom:"",
				msgcreator:""
			}
		},
		onShow(){
			this.getdata()	
			
		},	
		
		methods: {


			getdata(){
				// 调用接口
				uni.request({
					url:"http://api.txapi.cn/v1/c/love_talk",
					method:"GET",
					data:{
						token:"UYQYRDWNzL0OMN"
					},
					success:res=>{
						this.msg = res.data.data
					}
				})
				// uni.request({
				// 	url:"http://api.txapi.cn/v1/hitokoto",
				// 	method:"GET",
				// 	data:{
				// 		token:"UYQYRDWNzL0OMN"
				// 	},
				// 	success:res=>{
				// 		this.msg1 = res.data.data.content
				// 		this.msgfrom = res.data.data.from
				// 		this.msgcreator = res.data.data.creator
				// 	}
				// })			
			},
			getcarton(){
				uni.request({
					url:"http://api.txapi.cn/v1/hitokoto",
					method:"GET",
					data:{
						token:"UYQYRDWNzL0OMN"
					},
					success:res=>{
						console.log(res),
						this.msg1 = res.data.data.content
						this.msgfrom = res.data.data.from
						this.msgcreator = res.data.data.creator
					}
				})
			},
			next(){
				this.getdata()
			},
			next1(){
				this.getcarton()
			}
		}
	}
</script>

<style>
.title{
	text-align: center;
	color: pink;
	font-size: 50rpx;
	font-weight: bold;
}
.text{
	text-indent: 2em;
	margin: 0 20rpx;
}
.button1{
	margin: 0 0rpx;
}
</style>
