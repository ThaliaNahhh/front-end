# css
from 122 to 148

# 旋转
	//通过旋转可以使元素沿着x y z轴旋转指定的角度。
	rotateX() rotateY() rotateZ()
	eg. transform: rotateZ(.25turn);
		transform: rotateY(45deg) translateZ(100px);//先转再平移（往后转）
		transform:  translateZ(100px) rotateY(45deg);//先平移再转（往前转 更近））
		transform: rotateY(180deg); //翻转+透视
		backface-visibility: visible(/hidden);//是否显示元素背面

# 立方体
	//为元素设置透明效果
	opacity: 0.7;
	//设置3d变形效果
	transform-style:preserve-3d;	

# 缩放
	//对元素进行缩放的函数（可以用来做hover放大）：
		scaleX()
		scaleY()
		scale()
	//tips:scaleZ()比较少用，因为本质上是拉长Z轴。无立体结构看不出来。
	
	//变形原点：
	transform-orgin: 0 0;(默认值center)
# less
	//less：是一门css的预处理语言，css的增强版，代码更少，样式更强大。
1. 应用场景：
	同一颜色多处使用。
	```js
	html{
		--color:#ff0;
		--length:200px;
	}
	.box1{
		width:var(--length);
		height: var(--length);
		color:var(--color);
	}
	.box2{
		//calc()计算函数
		width:calc(200px*2);
		height: var(--length);
		background-color:var(--color);
	}
	```
