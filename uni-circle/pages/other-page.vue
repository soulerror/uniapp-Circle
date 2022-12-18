<template>
	<view class="pli-page">
		<view class="pli-head">
			Uni-Circle
		</view>
		<view class="pli-card">
			<view>
				<Circle  :percent="60" circleColor="cyan">
					<span slot="content">Cyan</span>
				</Circle>
				进度条颜色
			</view>
			
			<view>
				<Circle  :percent="60" defaultColor="black">
					<span slot="content">black</span>
				</Circle>
				圆环颜色
			</view>
			
			<view>
				<Circle  :percent="60" :circleWidth="10">
					<span slot="content">10px</span>
				</Circle>
				圆环宽度
			</view>
			
		</view>
	</view>
</template>

<script>

import Circle from "../components/Circle.vue"
	export default {
		components:{
			Circle
		},
		data() {
			return {
			}
		},
		methods: {

		},
		onShow() {
		}
	}
</script>

<style Scoped>
.pli-page{
	height: 100%;
	width: 100%;
}
.pli-head{
	height:40%;
	width: 100%;
	text-align:center;
	color: white;
	background:linear-gradient(to right,#1A79A0,#32CDA5);
}
.pli-card{
	width:calc(100% - 40px);
	margin: 0 auto;
	height: 70%;
	position: relative;
	top:-20%;
	border-radius: 5px;
	background-color: white;
	border: 2px #32CDA5 solid;
	display: flex;
	flex-direction:row;
	flex-wrap: wrap;
	justify-content: space-between;
	padding: 5px;
	font-size: 14px;
}
.pli-card view{
	text-align: center;
}
</style>
