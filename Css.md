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
> 变量语法：@变量名 @{变量名} 
> 使用变量时，若直接使用则直接 @变量名 使用即可。
> 作为类名或一部分值，需要 @{变量名} 的形式使用。
> 新版语法： $属性名 可用于直接调用上一个属性的值。

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
>     .p1() 直接对指定样式进行引用，相当于对p1样式进行复制。mixin混合。
    但是复制，性能较差。
```js
.p3{
    //.p1() 直接对指定样式进行引用，相当于对p1样式进行复制。mixin混合。
    //复制，性能更差。
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
