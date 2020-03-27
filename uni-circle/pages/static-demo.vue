<template>
	<view class="pli-page">
		<view class="pli-head">
			Uni-Circle
		</view>
		<view class="pli-card">
			<cCircle  :size="40" :percent="40"></cCircle>
			<cCircle  :size="45" :percent="45"></cCircle>
			<cCircle  :size="50" :percent="50"></cCircle>
			<cCircle  :size="55" :percent="55"></cCircle>
			<cCircle  :size="60" :percent="60"></cCircle>
			<cCircle  :size="65" :percent="65"></cCircle>
			<cCircle  :size="70" :percent="70"></cCircle>
			<cCircle  :size="100" :percent="100"></cCircle>
			<cCircle  :size="70" :percent="70">
				<span slot="content" style="text-align: center;">自定义文本</span>
			</cCircle> 
			<cCircle  :size="70" :percent="70">
				<img slot="content" style="height: 100%;width: 100%;border-radius: 50%;" src="/static/temp.jpg">
			</cCircle>
			<cCircle  :size="70" :percent="100">
				<span slot="content" style="text-align: center;">
					 <icon slot="content" type="success_no_circle" color="#32CDA5" size="26"/>
				</span>
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
