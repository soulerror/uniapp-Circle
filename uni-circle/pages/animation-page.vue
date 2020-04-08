<template>
	<view class="pli-page">
		<view class="pli-head">
			Uni-Circle
		</view>
		<view class="pli-card">

		 <cCircle  :size="60" :percent="60" :animation="true" :animationSpeed="1" >
				<span slot="content">1</span>
			</cCircle>
			<cCircle  :size="60" :percent="60" :animation="true" :animationSpeed="2">
				<span slot="content">2</span>
			</cCircle>
			<cCircle  :size="60" :percent="60" :animation="true" :animationSpeed="3">
				<span slot="content">3</span>
			</cCircle>
			<cCircle  :size="60" :percent="60" :animation="true" :animationSpeed="4">
				<span slot="content">4</span>
			</cCircle>
			<cCircle  :size="60" :percent="60" :animation="true" :animationSpeed="5">
				<span slot="content">5</span>
			</cCircle>
			<cCircle  :size="60" :percent="60" :animation="true" :animationSpeed="10">
				<span slot="content">10</span>
			</cCircle>
			<cCircle  :size="60" :percent="90" :animation="true" :animationSpeed="50">
				<span slot="content">50</span>
			</cCircle>
			<cCircle  :size="60" :percent="60" :animation="true" :animationSpeed="50" @onComplete="show" @animationPercent="getPercent">
				<!-- <span v-show="!showImg" slot="content">{{percent}}%</span> -->
				<img slot="content" style="height: 100%;width: 100%;border-radius: 50%;" src="/static/temp.jpg">
			</cCircle> 
			
		<cCircle  :size="60" :percent="60" :animation="true" :animationSpeed="100" @animationPercent="getPercent">
				<span slot="content" style="color: #32CDA5;">{{percent}}</span>
			</cCircle>

		</view>
	</view>
</template>

<script>

import cCircle from "../components/cCircle.vue"
	export default {
		components:{
			cCircle
		},
		data() {
			return {
				showImg:false,
				percent:0
			}
		},
		methods: {
			show(){
				console.log("执行完成");
				this.showImg=true;
			},
			getPercent(animationPercent){
				this.percent = animationPercent;
			}
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
