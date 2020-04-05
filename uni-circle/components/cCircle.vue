<template>
	<view>
		<view :style="cBox">
			<text v-if="!slot">{{animationPercent}}%</text>
			<view  :style="slotStyle" v-if="slot"><slot name="content"></slot></view>
			<view  :style="faStyle">
				
				<view  :style="leftStyle"></view>
				 <view :style="rithStyle"></view>
			</view>
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
						that.$emit('onComplete');
					}
					else{
						that.animationPercent+=1;
						that.$emit('animationPercent',that.animationPercent);
					}
					
				},that.animationSpeed);
			},

			
		},
		props:{
			//大小
			size:{
				type:Number,
				default:60
			},
			//进度条颜色
			circleColor:{
				type:String,
				default:'#32CDA5'
			},
			//圆环背景色
			defaultColor:{
				type:String,
				default:'#e9e9e9'
			},
			//圆环宽度
			circleWidth:{
				type:Number,
				default:5
			},
			//百分比
			percent:{
				type:Number,
				default:0
			},
			//动画效果
			animation:{
				type:Boolean,
				default:false
			},
			//帧动画间隔
			animationSpeed:{
				type:Number,
				default:1
			},
			//动画方向
			clockwise:{
				type:Boolean,
				default:true
			},
			//自定义七点位置
			direction:{
				type:Number,
				default:0
			}
		},
		computed:{
			slot(){
				
				if(this.$slots.content){
					return true;
				}
				return false;
			},
			cBox(){
				
				var size=this.size;
				var circleWidth = this.circleWidth;
				var style=
					`	
						position:relative !important;
						height:${circleWidth*2+size}px;
						width:${circleWidth*2+size}px;
						display:flex;
						justify-content: center;
						align-items: center;
					`;
					return style;
			},
			slotStyle(){
				var size=this.size;
				var circleWidth = this.circleWidth;
				var style=
					`
						border-radius:50%;
						height:${size}px;
						width:${size}px;
						display:flex;
						justify-content: center;
						align-items: center;
					`;
					return style;
			},
			faStyle(){
				var size= this.size;
				var circleWidth = this.circleWidth;
				var defaultColor = this.defaultColor;
				var direction = this.direction;
				var clockwise = this.clockwise;
				var style = `
							 position:absolute !important;
							 border-radius:50%;
							 display:flex;
							 justify-content: center;
							 align-items: center;
							 height:${size}px;
							 width:${size}px;
							 border:${circleWidth}px ${defaultColor} solid;
							 transform:rotate(${direction}deg) rotateY(${clockwise?0:180}deg);
							 
							`;
				return style;
			},
			leftStyle(){
				var top = this.top;
				var clockwise = this.clockwise;
				var size = this.size;
				var circleColor = this.circleColor;
				var circleWidth = this.circleWidth;
				var percent = this.animation?this.animationPercent:this.percent;
				var style;
				style= `
					height:${size}px !important;
					width:${size}px !important;
					border:${circleWidth}px ${circleColor} solid !important;
					border-radius:50% !important; 
					z-index:0 !important;
					position:absolute !important;
					top:-{circleWidth}px;
					left:-{circleWidth}px;
					transform:rotate(${percent>50?180:(percent/100*360)}deg) !important;
					clip:rect(0 ${circleWidth*2+size}px ${circleWidth*2+size}px ${(circleWidth*2+size)/2}px ) !important;
					`;
				return style;
			},
			rithStyle(){
				
				var direction = this.direction;
				var size = this.size;
				var circleColor = this.circleColor;
				var defaultColor = this.defaultColor;
				var circleWidth = this.circleWidth;
				var percent = this.animation?this.animationPercent:this.percent;
				var style= `
							 height:${size}px !important;
							 width:${size}px !important;
							 border:${circleWidth}px ${percent>50?circleColor:defaultColor} solid !important;
							 border-radius:50% !important;
							 z-index:${percent>50?0:10} !important;
							 position:absolute !important;
							 top:-{circleWidth}px;
							 right:-{circleWidth}px;
							 transform:rotate(${percent>50?percent/100*360:0}deg) !important;
							 clip:rect(0 ${circleWidth*2+size}px ${circleWidth*2+size}px ${(circleWidth*2+size)/2}px ) !important; 
							`;

				return style;
			}
		}
	}
</script>