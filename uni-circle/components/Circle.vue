<template>
  <view>
    <view :style="cBox">
      <text v-if="!$slots.content">{{ animationPercent }}%</text>
      <view :style="slotStyle" v-if="$slots.content"
        ><slot name="content"></slot
      ></view>
      <view :style="faStyle">
        <view :style="leftBox">
          <view :style="leftStyle"></view>
        </view>
        <view :style="rithStyle"></view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      animationPercent: 0,
    };
  },
  mounted() {
    if (this.animation) {
      this.loadAnimation();
    } else {
      this.animationPercent = this.percent;
    }
  },
  methods: {
    //动画加载方法
    loadAnimation() {
      this.animationPercent = 0;
      let that = this;
      let timer = setInterval(() => {
        if (that.animationPercent >= that.percent) {
          clearInterval(timer);
          that.$emit("onComplete");
        } else {
          that.animationPercent += 1;
          that.$emit("animationPercent", that.animationPercent);
        }
      }, that.animationSpeed);
    },
  },
  props: {
    //大小
    size: {
      type: Number,
      default: 60,
    },
    //进度条颜色
    circleColor: {
      type: String,
      default: "#32CDA5",
    },
    //圆环背景色
    defaultColor: {
      type: String,
      default: "#e9e9e9",
    },
    //圆环宽度
    circleWidth: {
      type: Number,
      default: 5,
    },
    //百分比
    percent: {
      type: Number,
      default: 0,
    },
    //动画效果
    animation: {
      type: Boolean,
      default: false,
    },
    //帧动画间隔
    animationSpeed: {
      type: Number,
      default: 1,
    },
    //动画方向
    clockwise: {
      type: Boolean,
      default: true,
    },
    //自定义七点位置
    direction: {
      type: Number,
      default: 0,
    },
  },
  computed: {
    sizeAdapter() {
      return this.size % 2 == 0 ? this.size : this.size - 1;
    },
    cBox() {
      let size = this.sizeAdapter;
      let circleWidth = this.circleWidth;
      let style = `	
						position:relative !important;
						height:${circleWidth * 2 + size}px !important;
						width:${circleWidth * 2 + size}px !important;
						display:flex !important;
						justify-content: center !important;
						align-items: center !important;
					`;
      return style;
    },
    slotStyle() {
      let size = this.sizeAdapter;
      let style = `
						border-radius:50% !important;
						height:${size}px !important;
						width:${size}px !important;
						display:flex !important;
						justify-content: center !important;
						align-items: center !important;
					`;
      return style;
    },
    faStyle() {
      let size = this.sizeAdapter;
      let circleWidth = this.circleWidth;
      let defaultColor = this.defaultColor;
      let direction = this.direction;
      let clockwise = this.clockwise;
      let style = `
							 position:absolute !important;
							 border-radius:50% !important;
							 display:flex !important;
							 justify-content: center !important;
							 align-items: center !important;
							 top:0 !important;
							 left:0 !important;
							 height:${size}px !important;
							 width:${size}px !important;
							 border:${circleWidth}px ${defaultColor} solid !important;
							 transform:rotate(${direction}deg) rotateY(${
        clockwise ? 0 : 180
      }deg) !important;
							`;
      return style;
    },
    leftBox() {
      let size = this.sizeAdapter;
      let circleWidth = this.circleWidth;
      let style = `
					height:${circleWidth * 2 + size}px !important;
					width:${circleWidth * 2 + size}px !important;
					position:absolute !important;
					top:-${circleWidth}px !important;
					left:-${circleWidth}px !important;
					opacity:1 !important;
					clip:rect(0 ${(circleWidth * 2 + size) / 2}px ${
        circleWidth * 2 + size
      }px 0) !important;
				`;
      return style;
    },
    leftStyle() {
      let size = this.sizeAdapter;
      let circleColor = this.circleColor;
      let circleWidth = this.circleWidth;
      let percent = this.animation ? this.animationPercent : this.percent;
      let style;
      style = `
					height:${size}px !important;
					width:${size}px !important;
					border:${circleWidth}px ${circleColor} solid !important;
					border-radius:50% !important; 
					z-index:0 !important;
					position:absolute !important;
					top:0px !important;
					left:0px !important;
					transform:rotate(${percent > 50 ? 180 : (percent / 100) * 360}deg) !important;
					clip:rect(0 ${circleWidth * 2 + size}px ${circleWidth * 2 + size}px ${
        (circleWidth * 2 + size) / 2
      }px ) !important;
					`;
      return style;
    },
    rithStyle() {
      let size = this.sizeAdapter;
      let circleColor = this.circleColor;
      let defaultColor = this.defaultColor;
      let circleWidth = this.circleWidth;
      let percent = this.animation ? this.animationPercent : this.percent;
      let style = `
							 height:${size}px !important;
							 width:${size}px !important;
							 position:absolute;
							 border:${circleWidth}px ${
        percent > 50 ? circleColor : defaultColor
      } solid !important;
							 border-radius:50% !important;
							 z-index:${percent > 50 ? 0 : 100} !important;
							 position:absolute !important;
							 top:-${circleWidth}px;
							 left:-${circleWidth}px;
							 transform:rotate(${percent > 50 ? (percent / 100) * 360 : 0}deg) !important;
							 clip:rect(0 ${circleWidth * 2 + size}px ${circleWidth * 2 + size}px ${
        (circleWidth * 2 + size) / 2
      }px ) !important; 
							`;

      return style;
    },
  },
};
</script>
