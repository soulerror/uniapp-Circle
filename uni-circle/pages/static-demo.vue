<template>
	<view class="pli-page">
		<view class="pli-head">
			Uni-Circle
		</view>
		<view class="pli-card">
			<Circle  :size="40" :percent="10" ></Circle>
			<Circle  :size="40" :percent="40" ></Circle>
			<Circle  :size="45" :percent="45" ></Circle>
			<Circle  :size="50" :percent="50" ></Circle>
			<Circle  :size="55" :percent="55"></Circle>
			<Circle  :size="60" :percent="60"></Circle>
			<Circle  :size="65" :percent="65"></Circle>
			<Circle  :size="70" :percent="70"></Circle>
			<Circle  :size="100" :percent="100"></Circle>
			<Circle  :size="70" :percent="70">
				<span slot="content">Circle</span>
			</Circle> 
			<Circle  :size="70" :percent="70">
				<img slot="content" style="height: 100%;width: 100%;border-radius: 50%;" src="/static/temp.jpg">
			</Circle>
			<Circle  :size="70" :percent="100">
				<span slot="content" style="text-align: center;">
					 <icon slot="content" type="success_no_circle" color="#32CDA5" size="26"/>
				</span>
			</Circle> 
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
				percent:50
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
}
</style>
