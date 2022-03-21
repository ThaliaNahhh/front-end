# css
from 122 to 148

旋转
	通过旋转可以使元素沿着x y z轴旋转指定的角度。
	rotateX() rotateY() rotateZ()
	eg. transform: rotateZ(.25turn);
		transform: rotateY(45deg) translateZ(100px);//先转再平移（往后转）
		transform:  translateZ(100px) rotateY(45deg);//先平移再转（往前转 更近））
		transform: rotateY(180deg); 翻转+透视
		backface-visibility: visible(/hidden);//是否显示元素背面

立方体：
	//为元素设置透明效果
	opacity: 0.7;
	//设置3d变形效果
	transform-style:preserve-3d;	

