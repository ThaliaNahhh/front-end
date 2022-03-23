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
	> less：是一门css的预处理语言，css的增强版，代码更少，样式更强大。
	> less中添加了许多新特性。eg.对变量的支持，对mixin的支持。
	> less语法和css语法大体上一致，但有许多扩展。所以浏览器无法直接执行less代码。
			需要插件转换而后由浏览器执行。
	> 	// less中的单行注释, 不会被解析到css中。
		/*  css中的注释，
			会被解析到css中。
		*/
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
2.变量

	> 变量：在变量中可以存储一个任意值，并在需要时任意修改。
		变量发生重名时，优先使用更近的。
		可以在变量声明前使用但不建议。
	  //变量语法：@变量名 @{变量名} 
	  //使用变量时，若直接使用则直接 @变量名 使用即可。
	  //作为类名或一部分值，需要 @{变量名} 的形式使用。
	  //新版语法： $属性名 可用于直接调用上一个属性的值。

```js
	@a:100px;
	@b:#bfa;
	@c:box6;

	.box5{
		width: @a;
		color: @b;
	}

	.@{c}{
		width: @a;
		height: $width;
		background-image: url("@{c}/1.png");
	}

	.box5 {
	  width: 100px;
	  color: #bfa;
	}
	.box6 {
	  width: 100px;
	  height: 100px;
	  background-image: url("box6/1.png");
	}
```

3. 父元素和扩展
> & 表示外层父元素。


```js
	>.box3{
        /*子元素选择器*/
        background-color: aqua;
        &:hover{
            color: orange;
        }
    }

   
    &:hover{
        color: orange;
    }

	.box1 > .box3 {
	  /*子元素选择器*/
	  background-color: aqua;
	}
	.box1 > .box3:hover {
	  color: orange;
	}
	.box1:hover {
	  color: orange;
	}
```

> :extend() 表示对当前选择器扩展指定选择器的样式。

```js
.p1{
    width: 100px;
    height: 100px;
}

.p2:extend(.p1){
    color: red;
}


.p1,
.p2 {
  width: 100px;
  height: 100px;
}
.p2 {
  color: red;
}
```
> .p1() 直接对指定样式进行引用，相当于对p1样式进行复制。mixin混合.
	//但是复制，性能较差。
```js
.p3{
    .p1();
}

.p3 {
  width: 100px;
  height: 100px;
}
```

> 使用类选择器时可以在选择器后边添加一个括号，实现mixin，给别人使用。

```js
.p4(){
    width: 100px;
    height: 100px;
}
.p5{
    .p4;
}
	
.p5 {
  width: 100px;
  height: 100px;
}
```
4. 混合函数

	 - 在混合函数中可以直接设置变量。
	 - 调用时按顺序传参。
	 - 可以指定默认值，不传值时使用默认值。
	 - 一些函数：average(#000, #fff); darken(#bfa);
```js
.test(@w:200px , @h:200px, @bg-color:#bfa){
	width: @w;	width: @w;
	height:@h;
	background-color: @bg-color;
}
div{
	.test(200px, 100px, red);
	.test(@bg-color:red, @w: 100px, @h: 100px);
	.test(200px);//其余的使用默认值
}

```
5. 补充

	- 通过 @import 来引入其他样式设置。
	- 在less中可以进行数值运算。
  
# flex

> 1. 概念
	
	flex(弹性盒、伸缩盒)：
		- 是css中的有一种布局手段，主要用来代替浮动来完成页面布局；
		- 可以使得元素具有弹性，让元素可以根据页面大小改变而改变。
		- 弹性容器
			- 要使用弹性盒，必须通过display先将一个元素设置为弹性容器。
			display: flex 设置为块级
			display: inline 设置为行内
		- 弹性元素（弹性项），弹性容器的子元素
			- 弹性元素可以同时是弹性容器
> 2. 设置
	
	弹性容器的属性：
	flex-direction 指定容器中弹性元素的排列方式。
		可选值：row(默认)， 水平排列（左->右）
				row-reverse 
				column
				column-reverse
		主轴：弹性元素的排列方向。
		侧轴：与主轴垂直的轴。
	flex-wrap: 设置弹性元素是否在弹性容器中换行
		nowrap：默认值，元素不会自动换行
		wrap: 元素沿辅轴方向自动换行。
		wrap-reverse: 元素沿辅轴反方向自动换行。
		
	flex-flow: wrap 和 direction 的简写属性。
	
	justify-content：如何分配主轴上的空白区间。
		flex-start:元素沿着主轴起边排列。
		flex-end:元素沿着主轴终边排列。
		center:居中。
		space-around:空白分布到元素两侧。
		space-evenly:空白分布到元素单侧。
		
	align-items:元素在辅轴上如何对齐以及元素之间的关系。
		strech 默认 将元素的长度设置为相同的值。
		flex-start 不拉伸 沿着辅轴起边对齐。
		flex-end 不拉伸 沿着辅轴终边对齐。
		center 居中。
		baseline 基线对齐。
	
	align-content：辅轴空白区间的分布。
		center
		flex-start 
		flex-end 
		space-between
		
	align-self: 用来覆盖当前弹性元素上的空白区间分布。
	
	弹性元素的属性：
	
	flex-grow：指定弹性元素的伸展系数，默认0；
		- 当父元素有多余空间时，子元素伸展方式。
		- 父元素的剩余空间按照比例进行分配。
	flew-shrink: 指定弹性元素的收缩系数, 计算方式较复杂，根据缩减系数和元素大小来计算。
		- 当父元素空间不足以容纳所有子元素时，子元素的收缩方式。
		
	flex-basis: 元素在主轴上的基础长度（制定了宽度/高度）。
		auto: 默认，参考元素自身宽高度。
		
	flex: 简写三样式 增长 缩减 基础。
		initial “flex: 0 1 auto”.仅减
		auto “flex: 1 1 auto”.
		none “flex: 0 0 auto”.无弹性
		
	order:决定元素的排列顺序。

# 像素

1. 像素
	- 屏幕是由若干发光小点（像素）构成。
	- 分辨率：1920X1080，是说屏幕中像素的数量。
	- 前端开发中像素分成两种：css像素和物理像素，浏览器在显示网页时，将css像素转换成物理像素而后呈现。
		一个css像素最终由几个物理像素呈现，由浏览器控制。默认下 pc端一个css像素=一个物理像素。
	
	
2. 视口（viewport）
	- 视口就是屏幕中用来显示网页的区域，可以通过查看视口大小得到css/物理的像素比值
	- 默认情况下 
		视口宽度： 1920px（css） 物理像素（1920px） 1:1
	- 放大情况下 
		视口宽度： 980px（css） 物理像素（1920px） 1:2

3. 移动端
	- 不同的屏幕单位像素大小不同，像素越小屏幕越清晰。智能手机的像素点远远小于计算机的像素点。
	- 问题：一个宽度为990px的网页在iphone6（750x1334）中如何显示呢？
		默认情况下，移动端网页都会将视口设置为980像素（css像素），以确保pc端网页可以在移动端正常访问。
		但是如果网页宽度超过980，移动端浏览器将会自动缩放以完整显示。
		
		所以大部分pc端网站都可以在移动端中正常浏览， 但体验较差。
		
		为了解决这个问题，大部分网站会专门给移动端设计网站。
	- 默认情况下， 移动端像素比是 980/移动端宽度（980/750）。
		若直接在网页中编写移动端代码，则像素比（1:0.~）会导致看到的内容过小。
		所以编写时， 必须有一个比较合理的像素比。
			1css 对应 2（或3）个物理像素
	- 可以通过meta标签设置视口大小
		```<meta name="viewpoint" content="width=300px">```
		每款移动设备设计时都会有一个最佳像素比，可以直接将其设置为该值，该视口大小称为完美视口
		device-width表示设备宽度（完美视口）。
		
		将网页的视口设置为完美视口（用于移动端）：
		```<meta name="viewport" content="width=device-width, initial-scale=1.0">```
		
		
