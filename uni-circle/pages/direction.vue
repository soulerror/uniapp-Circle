<template>
	<view class="pli-page">
		<view class="pli-head">
			Uni-Circle
		</view>
		<view class="pli-card">
			<view style="width: 100%;">顺时针</view>
			<cCircle  :size="60" :percent="50" :direction="30" :animation="true" :animationSpeed="50">
				<span slot="content">30</span>
			</cCircle>
			<cCircle  :size="60" :percent="50" :direction="60" :animation="true" :animationSpeed="50">
				<span slot="content">60</span>
			</cCircle>
			<cCircle  :size="60" :percent="50" :direction="90" :animation="true" :animationSpeed="50">
				<span slot="content">90</span>
			</cCircle>
			<cCircle  :size="60" :percent="50" :direction="180" :animation="true" :animationSpeed="50">
				<span slot="content">180</span>
			</cCircle>
			<view style="width: 100%;">逆时针</view>
			<cCircle  :size="60" :percent="50" :direction="30" :animation="true" :clockwise="false" :animationSpeed="50">
				<span slot="content">30</span>
			</cCircle>
			<cCircle  :size="60" :percent="50" :direction="60" :animation="true" :clockwise="false" :animationSpeed="50">
				<span slot="content">60</span>
			</cCircle>
			<cCircle  :size="60" :percent="50" :direction="90" :animation="true" :clockwise="false" :animationSpeed="50">
				<span slot="content">90</span>
			</cCircle>
			<cCircle  :size="60" :percent="50" :direction="180" :animation="true" :clockwise="false" :animationSpeed="50">
				<span slot="content">180</span>
			</cCircle>
			<cCircle  :size="60" :percent="60" :direction="180" :animation="true" :animationSpeed="50" @onComplete="show" >
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
