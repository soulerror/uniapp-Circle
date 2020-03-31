# uniapp-Circle
uniapp插件：基于CSS实现的进度环

## **使用方法**：
#### **1.复制components目录下面的vue文件,到你的项目中**
#### **2.在需要你需要使用的地方引入,例如**
###### `import cCircle from "../components/Your_Exios-Circle.vue"`
#### **3.注册组件**
```	
export default {
		components:{
			cCircle
		},
		data() {
			return {
			
			}
		}
	} 
```
#### **4.在项目中使用**
```
<template>
	<view >
	 <cCircle  :size="60" :percent="60"></cCircle>
	</view>
</template>
```

###**属性文档**

| 属性           | 名称         |  类型   | 默认值  | 备注                                          |
| -------------- | ------------ | :-----: | ------- | :-------------------------------------------- |
| size           | 圆环大小     | Number  | 60      | 单位px                                        |
| percent        | 百分比       | Number  | 0       | 0-100的整数，暂不支持小数                     |
| circleColor    | 进度环颜色   | String  | #32CDA5 | 支持rgba写法，进度条颜色，百分比为0时，不显示 |
| defaultColor   | 进度环背景色 | String  | #e9e9e9 | 支持rgba，圆环默认颜色，百分比为100时，不显示 |
| circleWidth    | 圆环宽度     | String  | 5       | 单位px                                        |
| animation      | 加载动画     | Boolean | false   | 是否开启动画加载，默认不开启                  |
| animationSpeed | 动画速度     | Number  | 1       | 动画的加载间隔速度，默认1ms,值越大，加载越慢  |

#### **使用注意事项**
有同学加我QQ，问我为什么定义自定义颜色的时候，报错了，她的代码是这样的
```
<cCircle  :size="60" :percent="60" :circleColor="#32CD45"></cCircle>
```
然后编译报错了
这位童鞋的前端基础，可能稍稍有点儿薄弱。
问题的原因是，Vue的机制是，属性前面加了" : "，那么" = "号后面的值，会被当做表达式，如果不加，则被当做字符串。
这里因为circleColor需要的值，本来就是String类型的，而不是表达式，所以这里就不用加了。

###**事件文档**

| 事件名           |                  说明                  | 参数 | 返回值           | 备注                                                         |
| ---------------- | :------------------------------------: | ---- | :--------------- | ------------------------------------------------------------ |
| onComplete       |           动画加载完成时触发           | 无   | 无               | 无                                                           |
| animationPercent | 执行动画时，动态返回当前时刻的百分比值 | 无   | animationPercent | 返回的时间间隔是基于属性中的animationSpeed的值，例如animationSpeed的值为1ms，那么在加载动画时，则每过1ms执行一次函数，返回一次当前animationPercent的值 |

####**事件示例**

###### **@onCompelete事件**
```
<template>
    <cCircle  :size="60" :percent="60" :animation="true" :animationSpeed="50" @onComplete="testMethod></cCircle>
</template>
<script>
import cCircle from "../components/cCircle.vue"
	export default {
		components:{
			cCircle
		},
		data() {
			return {
				hehe:null
			}
		},
		methods: {
			testMethod(){
				console.log("执行完成");
			}
		},
	}
</script>
```
##### **效果**
![此处输入图片的描述][1]

###### **@animationPercent事件**
```
<template>
    <cCircle  :size="60" :percent="60" :animation="true"  :animationSpeed="100"
    @animationPercent="getPercent">
		<span slot="content" style="color: #32CDA5;">{{percent}}</span>
	</cCircle> 
</template>
<script>
import cCircle from "../components/cCircle.vue"
	export default {
		components:{
			cCircle
		},
		data() {
			return {
			    percent：0
			}
		},
		methods: {
			getPercent(animationPercent){
				this.percent = animationPercent;
			}
		},
	}
</script>
```

##### **效果**
![此处输入图片的描述][2]

### **拓展插槽**
###### 具名插槽**：content**
###### 作用：自定义显示圆环中央的文本
###### 例如：在圆环中央，不显示百分比，显示“Circle”字样：
```
<cCircle>
 <span slot="content" style="text-align: center;">Circle</span>
</cCircle> 
```

### 其他可能遇到的问题：
#### 动画加载方案：
动画通过js定时器实现，传入的animationSpeed则是定时器的间隔时间，传入的值越大，那么动画加载完成的时间越长。默认在组件的mounted生命周期中调用。在Uniapp中，有的页面会只会加载一次，然后常驻，那么动画只会出现一次。比如，首页在不退出应用的情况下，通常就只加载一次，那么动画只会加载一次。如果在某个子页面调用了cCircle组件，进入该页面时，会加载，退出该页面时，销毁了该页面，那么下次进入这个页面时，动画会再次加载。如果不能满足你的需求，可以自己修改代码，根据你的需求，自己定制。
#### 样式：
样式是通过computed属性动态计算的样式，在极个别情况下，会受到外部元素的样式污染。如果遇到你遇到了样式污染的问题，可以尝试着修改一下父元素的样式，或者重写组件的样式，或者可以直接修改源码。

### 作者寄语：
作者QQ：1107837746

如果有什么问题、意见或建议可以加作者QQ沟通。如果我有时间和能力的话，一定解决。

不满足你的需求，可以任意修改，组件很简单，修改起来也不复杂。

作者是一个菜鸟Java开发，偶尔鼓捣鼓捣前端，因为发现Uniapp插件市场没有能够满足自己需求的插件，所以本着 “自己动手，丰衣足食” 的理念，动手写了组件。其实 作者前端技术比较一般，如果组件中有什么问题，欢迎指正，一定虚心学习。如果能够满足你的需求，欢迎到Github给作者Star：https://github.com/YourExios/uniapp-Circle


[1]: http://app.maikasai.com/onCompleteDemo.gif
[2]: http://app.maikasai.com/animationPercent.gif