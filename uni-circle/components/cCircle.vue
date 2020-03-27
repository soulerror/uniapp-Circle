<template>
	<view>
		<view  :style="faStyle">
			<text v-if="slot">{{animationPercent}}%</text>
			<slot name="content"></slot>
			<view  :style="leftStyle"></view>
			<view :style="rithStyle"></view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				animationPercent:0
			};
		},
		mounted() {
			if(this.animation){
				this.loadAnimation();
			}
			else{
				this.animationPercent=this.percent;
			}
		},

		methods:{
			//动画加载方法
			loadAnimation(){
				this.animationPercent = 0;
				var that = this;
				var i = setInterval(()=>{
					if(that.animationPercent>=that.percent){
						clearInterval(i);
					}
					else{
						that.animationPercent+=1;
					}
					
				},that.animationSpeed);
			}
		},
		props:{
			size:{
				type:Number,
				default:60
			},
			circleColor:{
				type:String,
				default:'#32CDA5'
			},
			defaultColor:{
				type:String,
				default:'#e9e9e9'
			},
			circleWidth:{
				type:Number,
				default:5
			},
			percent:{
				type:Number,
				default:0
			},
			animation:{
				type:Boolean,
				default:false
			},
			animationSpeed:{
				type:Number,
				default:1
			}
		},
		computed:{
			slot(){
				if(this.$slots.content){
					return false;
				}
				return true;
			},
			faStyle(){
				var size= this.size;
				var circleWidth = this.circleWidth;
				var defaultColor = this.defaultColor;
				var style = `
							 position:relative;
							 border-radius:50%;
							 display:flex;
							 justify-content: center;
							 align-items: center;
							 height:${size}px;
							 width:${size}px;
							 border:${circleWidth}px ${defaultColor} solid;
							`;
				return style;
			},
			leftStyle(){
				var size = this.size;
				var circleColor = this.circleColor;
				var circleWidth = this.circleWidth;
				var percent = this.animation?this.animationPercent:this.percent;
				var style = `
							 height:${size}px;
							 width:${size}px;
							 border:${circleWidth}px ${circleColor} solid;
							 border-radius:50%; 
							 z-index:0;
							 position:absolute;
							 transform:rotate(${percent>50?180:(percent/100*360)}deg);
							 clip:rect(0 ${circleWidth*2+size}px ${circleWidth*2+size}px ${(circleWidth*2+size)/2}px ); 
							`;
				
				return style;
			},
			rithStyle(){
				var size = this.size;
				var circleColor = this.circleColor;
				var defaultColor = this.defaultColor;
				var circleWidth = this.circleWidth;
				var percent = this.animation?this.animationPercent:this.percent;
				var style = `
							 height:${size}px;
							 width:${size}px;
							 border:${circleWidth}px ${percent>50?circleColor:defaultColor} solid;
							 border-radius:50%;
							 z-index:${percent>50?0:1};
							 position:absolute;
							 transform:rotate(${percent>50?percent/100*360:0}deg);
							 clip:rect(0 ${circleWidth*2+size}px ${circleWidth*2+size}px ${(circleWidth*2+size)/2}px ); 
							`;
				
				return style;
			}
		}
	}
</script>