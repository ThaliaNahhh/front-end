# JS

1. 基础知识：
		
		编写位置：
		
			- 标签的onclick属性中，点击执行；
			- 超链接的href属性中，点击执行；
			- 但过于耦合，以上不建议。
			- 写在script标签或者js文件中。 script标签一旦用于引入外部，则无法编写内部代码。（可重开）

		注释：单行+多行。

		语法：严格区分大小写；每一条语句以分号结尾；忽略多个换行和空格符。

		字面量和变量：
			- 字面量：不可变值，可直接使用（一般不用）。
			- 变量：可变，用于保存字面量；用var关键字来声明。

		标识符：
			- 所有可以自主命名的，如：变量名、函数名、属性名等。
			- 命名规则（可以含有字母\数字\_\$;不能以数字开头；不能使关键字或保留字；驼峰命名法）

6. JS数据类型（六种：String Number Boolean Null Undefined Object）
		
		- typeof 变量： 用于检查变量类型；
		- String: 字符串 单引号或双引号引起，不要混用，无法嵌套；可使用\作为转义字符，用于表示特殊字符。 
		- Number：数值，整数和浮点数。整数运算基本保证精确，若浮点运算则不一定（0.1+0.2）
					Number.MAX_VALUE:表示数字最大值；若更大 则表示Infinity（正无穷）；
					Number.MIN_VALUE:表示零以上最小值。
					NaN: 特殊数值，表示not a number。
		- Boolean: 布尔值（true false）
		- Null: 仅有一个值：null，用于表示一个为空的对象（object），typeof检查返回object。
		- Undefined: 仅有一个值， undefined, 表示一个声明但未赋值的对象。
			以上五种是基本数据类型。
		- Object: 引用数据类型。

7. 强制类型转换：

		- 将其他数据类型转换为：String、Number、Boolean.
		- 转换为String：
				1.调用被转换数据类型的toString（）方法，该方法不会影响原变量。null和undefined没有该方法。
				2.调用String()函数，被转换数据作为参数传入。对于number和boolean无影响，实际就是调用toString（）。
					对于null和defined，将其转换为“null”和“undefined”。
		- 转换为Number：
				1.调用Number()函数，被转换数据作为参数传入。
					字符串->数字，若为纯数字字符串，直接转为数字；若有非数字内容，则NaN；若空串或全空格，则转为0；
					布尔->数字，t：1；f:0;
					null->数字，0；
					undefined->数字， NaN；
				2.parseInt()：把一个字符串转为整数；parseFloat(): 转为浮点数。将一个字符串中的有效数值内容取出来转为Number。
					从左往右读。
					若对非String使用以上函数，则先将其转换为String再操作。
				3.其他进制：16进制：0x开头。8进制：0开头。二进制：0b开头（但不是所有浏览器都支持）。
					- 像070这种字符串，不同浏览器解析选择的进制不同（8或10）。所以为了统一，可以在parseInt()函数里多传一个参数。
		- 转换为Boolean：
				1. Boolean()函数：
					数字->布尔：除了0和nan，其余都是true；
					字符串->布尔，除空串其余都是true；
					null和undefined都是false；对象也是true。
				2. 隐式：可以对任意值取两次反。
					
8. 运算符：也叫操作符，可以对值进行运算获取结果。eg.typeof（获得值的类型并以字符串形式返回）。

		- 算数运算符（+-*/%）:二元运算符（需要两个操作数）
								当对非Number值进行运算时，会将其转换为Number再计算。
								任何值与NaN运算结果都为NaN。
						+ ：若对两个字符串进行加和计算，会进行拼串操作；任何值和字符串加和运算，都先转字符串而后拼串。
							（可利用这一特点隐式将任意数据类型转为String：c+"", 底层也是调用String）
						- * /: 任何值和字符串运算，都先把字符串转换成Number而后计算。实现隐式转换（-0， *1 , /1）
						%:取模
		- 一元运算符： +：正号
					   -：负号：对数字进行负号取反。
					   对于非Number，可以使用+号来改变数据类型。
		- 自增和自减：++a与a++。
		- 逻辑运算符： ！	非：对布尔值进行取反操作。若进行两次，无变化。若对非布尔值进行该操作，先转换为布尔再操作。
					   &&	与（短路与，若第一个为false则不会看第二个）：若对非布尔值进行该操作，先转换为布尔再操作。并且返回原值。
								与运算：若第一个值为true返回后面的， 若为false则返回靠前的值。
					   ||	或（短路或，若第一个为true则不会看第二个）：若对非布尔值进行该操作，先转换为布尔再操作。并且返回原值。
								或运算：若第一个值为false返回后面的， 若为true则返回靠前的值。
		- 赋值运算符： =：将符号右侧的值赋给左侧变量。
					   +=, -=, *=, /= , %=.
		- 关系运算符： >, >=, <, <=, ==:判断两个值的大小关系，返回true or false。
						非数值比较时会把其转换为数字再比较；任何值与NaN比较结果都为false。
						如果符号两侧的值都是字符串，不会转换为数字，而是比较其中unicode，
						按位比较，若两位一样则比较下一位。因此可以用来对字符串排序（比较中文没有意义）。
						因此，如果比较两个字符串型数字，必转型。
		- 相等运算符： ==：使用时，若两值类型不同，则会自动进行类型转换（一般是转为数字）。
						undefined衍生自null，这两个值相等判断返回true；
						nan不和任何值相等，包括它本身。（因此可以通过isNaN()函数判断一个值是否是NaN）。
					   !=:使用时，若两值类型不同，则会自动进行类型转换（一般是转为数字）。
					   ===：全等。用来判断两个值是否全等，与相等类似但不做类型转换。类型相同返回true。
					   !==: 不全等。用来判断两个值是否不全等，与不等类似但不做类型转换。类型不同返回true。
		- 条件运算符（三元运算符）：
						条件表达式？语句1：语句2；
						若条件表达式为非布尔值，会转为布尔值再运算。
		- ，运算符
		
9. 运算符优先级
	
		- 运算符优先级表
		- 括号改变优先级

10. 编码
	
	在字符串中使用\u来表示转义字符，输出Unicode编码；
		在网页中使用Unicode编码：&#编码(需要十进制)。

11. 语句
		
		执行顺序：从上至下；
		可以用{}为语句分组（代码块），同一个{}中的语句要么全执行，要么全不执行。{}后面的就不需要再写；了。
		{}只用于分组。
		
		- 流程控制语句：
			a. 条件判断语句（if-else if-else）
			b. 条件分支语句（switch，执行时依次进行全等比较）
			c. 循环语句（while；for；do...while）
			tips:网页换行使用<br/>；break可以用来终止循环。
		- break:终止靠自己最近的循环，可以为循环语句创建一个label来标识当前循环，
				使用break语句时，可以在break后面跟着一个label，这样break将会结束指定的循环。
		- continue:跳过当次循环，默认是离自己最近的循环。
		- console.time("计时器名字")。字符串可作为该计时器的标识符。
						可以用来计算时间，测试程序性能。
			console.timeEnd("计时器名字")， 用于结束计时器。

12. 输入
	
		- prompt()可以弹出一个提示框，该提示框会带有一个文本框，用户可以在文本框中输入一段内容；
			该函数需要一个字符串作为参数，该字符串将会作为提示框的提示文字。
			用户输入的内容将会作为函数返回值返回，可定义一个变量来接受该内容。（返回值为string）
		
13. 对象（Object）：引用数据类型，属于一种复合数据类型，保存多个不同数据类型属性。

		- 内建对象：由ES标准中定义的对象，任何ES的实现中都可以使用。eg.Math String Number Function Object...
		- 宿主对象：由JS的运行环境提供的对象，主要由浏览器提供的对象，如BOM，DOM（console.log()/document.write()）
		- 自定义对象：开发人员自己创建的对象。
		
		- 创建对象
			var obj = new Object();//使用new关键字调用的函数是构造函数constructor，
											是专门用来创建对象的函数。
									//对象中保存的值称为属性。
			var obj = {};		//使用对象字面量来创建一个对象。可以在创建对象时直接指定对象属性。
			var obj = {
						属性名:属性值,
						属性名:属性值,
						属性名:属性值
					};
		- 添加属性
			tips:对象属性名不强制要求遵守标识符规范，若要使用特殊属性名，语法也不同：
						语法：对象[”属性名"] = 属性值；读取时也类似。
				使用[]这种形式操作属性更加灵活。
			obj.name = "李四";		//向对象中添加属性，语法：对象.属性名 = 属性值；
									//读取对象中的属性：语法：对象.属性名
									//如果读取对象中没有的属性，不会报错而是返回undefined。
		
		- 删除属性 
			语法： delete 对象.属性名
			
		- 属性值：js对象的属性值可以是任意数据类型，包括对象。
		
		- 枚举属性：for(var 变量 in 对象){
					}
		- in运算符：通过该运算符可以检查一个对象中是否含有指定属性。
			语法： “属性名” in 对象；

14. 基本数据类型和引用数据类型（区别）

		- 内存管理：
			栈内存：JS中的变量都是保存在栈内存中的，基本数据类型直接在栈内存中存储，
						值之间独立存在，互不影响。
					变量 值
					
					a	 123
					b	 123
			堆内存：对象保存在堆内存中。
					var obj = new Object();
					如果一个obj复制了另一个obj的值，则两个obj的指向地址空间是同一个。
					obj是变量，保存在栈中，new Object()在堆内存中开辟新地址空间，将地址值赋给obj;
								
					变量 	值
					
					obj2	0x123
					obj1	0x123
			“深拷贝”“浅拷贝”；基本数据类型保存值，引用数据类型引用的是地址。
			
15. 函数（也是一个对象，网页中一切能看到的都是对象）
		
			可用于封装一些功能（代码），需要时执行（调用）这些功能。
			函数也可以作为参数传入函数，区别在于传的返回值还是函数本身。
		- 创建一个函数对象
			a.var fun = new function();	//typeof检查时会返回function。
					//可以将要封装的代码以字符串形式传递给构造函数。
			b.使用函数声明来创建一个函数：
				function fun2([形参1，形参2, ……]){
					console.log("hi!");
				}
				//调用函数时解析器不会检查实参类型，所以要注意是否会接收到非法参数。
				//调用函数时解析器不会检查实实参数量，多余实参不会被赋值；
								少于形参数量则对应的形参类型将是undefined。
			c.使用函数表达式来创建一个函数（将匿名函数赋值给一个变量）
				var 函数名 = function(){
					console.log("hi!");
				}
				
		- 调用一个函数对象			
			fun();	//调用语法： 函数对象();
			
		- 函数返回值
			使用return来设置函数返回值，其将作为函数执行结果返回。
			语法:
				return 值；	//return后不跟任何值时相当于返回undefined，若不写return也会返回undefined。
							//返回值可以是任何类型，函数也行。
		
		- 立即执行函数：函数定义完毕后立即被调用，往往只会执行一次，依托匿名函数。
			语法:
				eg.	(function(a, b){
				
					})(123,234);
					
16. 方法：函数作为对象的属性时，就是对象的方法。

17. JS中的作用域(作用域指一个变量的作用的范围)

		- 全局作用域：
			直接编写在script标签中的js代码都在全局作用域内；
			全局作用域在页面打开时创建，关闭时销毁；
			全局作用域中有一个全局对象window，代表浏览器窗口，由浏览器创建，可以直接使用；
			在全局作用域中，创建的变量都会作为window对象的属性保存，创建的函数都会作为window的方法保存；
			全局作用域中的变量都是全局变量，在页面的任意部分都可以访问。

		- 函数作用域（类似于小全局作用域）：
			调用函数时创建函数作用域，函数执行完毕后，作用域销毁；
			每调用一次函数都会创建一个新的函数作用域，它们之间相互独立；
			函数作用域内可以访问到全局作用域的变量，反之则不能；
			当在函数作用域中操作一个变量时，先在自身作用域中找，若无则找更外部的作用域，若再无则报错；
			函数中访问全局变量需使用window对象；
			函数作用域中也有声明提前特性，同样，函数声明也会在函数内最先执行；
			在函数中，不使用var声明的变量都会变成全局变量（d= 100相当于window.d=100）；
			定义形参相当于在函数作用域中声明变量，若未传参则变量为undefined。

		- 变量的声明提前：
			使用var关键字声明的变量会在所有代码执行之前被声明，但会在执行到当前行时赋值；
			如果声明变量时不适应var关键字则不会被声明提前。

		- 函数的声明提前：
			使用函数声明形式创建的函数 function 函数(){}，它会在所有代码执行之前就被创建（即声明提前，创建提前），因此可以在函数声明之前调用；
			使用函数表达式创建的函数不会被提前创建。


18. Debug
		
		打开浏览器-脚本（sources/调试程序）-打断点-监控
		单步跳过（F10）/添加监控/…

19. This

		- 解析器调用函数时，每次都会向函数内部传递进一个隐含的参数this，this指向的是一个对象，函数执行的上下文对象。
		- 根据函数的调用方式的不同，this指向不同的对象：
			1.以函数形式调用，this指向window；
			2.以方法形式调用，this指向调用方法的对象。
			3.当以构造函数形式调用，this指向新创建的对象。

		- 使用*工厂方法*创建对象可以提升代码复用率。
			'''js
			function createPerson(name, age,gender){
				var obj = new Object();
				obj.name=name;
				…
				return obj;
			}
			var obj1= createPerson(Thalia, 22, female);
			'''
		- 缺陷：使用的构造函数都是Object，因此创建的对象都是object类型，导致无法区分出多种不同类型的对象。(引出构造函数）

20. 构造函数

		- 构造函数是一个普通函数，创建方式和普通函数没有区别，习惯上首字母大写，用于创造不同的对象（如Person对象）。
		- 使用同一个构造函数创建的对象，我们称为一类对象，也将一个构造函数称为一个类（通过构造函数创建的对象称之为一个类的实例。


		- 构造函数与普通函数的区别：调用方式不同。
			构造函数：使用new关键字来调用。
			普通函数：直接调用。

		- 执行流程：
			1.立刻创建一个新的对象；
			2.将新建对象设置为函数中的this，在构造函数中可以使用this来引用新建的对象；
			3.逐行执行函数中代码；
			4.将新建对象作为返回值返回。

		'''js
			function Person(name, age,gender){
				this.name=name;
				…
			}
			var per1 = new Person(Thalia, 22, female);
			console.log(per1 instanceof Person); //使用instanceof检查一个对象是否是一个类的实例，是则true反之false。
					//所有对象都是object的后代，所以(对象 instanceof object)的答案都是true。
		'''
		
		- 缺陷
			在构造函数中为每一个对象都创造了一个新的方法，彼此独立；
			这导致所有实例的该方法都是唯一的，会浪费不少空间，因此应当使同样的方法公用。

		- 解决方法
			将公用方法放在全局作用域中定义, 但这污染了全局作用域的命名空间，并且不安全（引入原型）。


21. 原型Prototype

		- 解析器会给创建的每一个函数中添加一个属性prototype，该属性对应一个对象，即原型对象。
			当函数作为普通函数调用，prototype没有任何作用（指向原型对象）。
			当函数作为构造函数调用，它所创建的对象中都会有一个隐含属性，指向该构造函数的原型对象，通过__proto__来访问该属性。

		- 原型对象相当于一个公共区域，所有同一个类的实例都可以访问该原型对象。对象中共有的内容可以统一设置进原型对象中。
			创建构造函数时，可以将对象共有的属性和方法统一添加到构造函数的原型对象中。这样不必分别添加，也不会影响到全局作用域。
			
			eg.Myclass.prototype.a=123；

		- 访问对象的一个属性或者方法时，先在对象本身里去找，若没找到则去原型中找。
		
		- 使用in检查对象中是否有某个属性时，若自身没有但原型有也会返回true；
			因此可以使用对象的hasOwnProperty()来检查对象自身是否含有某个属性。
			
		- 原型对象也是对象，也有原型。当使用一个对象的属性或者方法时，先在自身找，若无则寻找原型或原型的原型，
			直至找到Object对象的原型。Object对象的原型不存在（null），若未找到则返回undefined。

			eg.console.log(my. __proto__. __proto__. __proto__);        //null


22. toString()

		- 当在页面打印一个对象时，实际上是输出的对象的toString()方法的返回值。
			若想修改输出对象结果，则可以为对象或原型添加一个toString()方法。
			Eg.[object Object]


23. 垃圾回收Garbage Collection

		- 程序运行中产生的垃圾
			当一个对象没有任何变量或属性对其引用，即无法操作，则成为垃圾，并且占有大量内存空间，导致程序运行变慢。

		- 垃圾回收机制 
			JS中拥有自动的垃圾回收机制，会自动将垃圾对象从内存中销毁，因此不需要也不能进行垃圾回收操作。
			因此只需将不需要使用的对象设置为null。


24. 内建对象：数组（Array）

		- 数组也是一个对象，和普通对象功能类似。数组中的元素可以是任意数据类型，包括函数或对象。
			区别在于普通对象的属性名是字符串，而数组使用数字索引来访问属性值（元素）；
					数组的存储性能比普通对象要好。

		tips: 面向对象：找对象->操作对象.
		
		- 创建数组
			a. 创建数组对象
				'''js
				var arr = new Array();		//创建数组对象
				arr[0]=10;					//向数组中添加元素
											//读取不存在的索引时，不会报错而是返回undefined
				console.log(arr.length);	//获取顺序添加的数组长度，非顺序添加的数组则会返回最大索引+1
				arr.length=10;				//修改length，若大于原数组则空出多余部分，若小于原数组则抛弃多余部分
				arr[arr.length]=8;			//向数组最后一位添加值
				'''
			
			b. 使用字面量来创建数组
				var arr=[1,2,3,4,5];		//可以在创建时就指定数组元素

			c. 使用构造函数创建数组
				var arr=new Array(1,2,3,4,5);	//可以在创建时就指定数组元素,将要添加的元素作为构造函数的参数传递，
												//但该形式用的不多，且只传一个数字表示指定数组长度。

			'''js
				arr=[[1,2,3],[2,3,4],[3,4,4]]	//二维数组
				console.log(arr);				//会把它拍扁
			'''
			
		- 数组的方法
			push();		//数组末尾添加n个元素并返回新长度
			pop();		//删除并返回数组最后一个元素。
			unshift();	//数组前端添加n个元素并返回新长度。
			shift();	//删除并返回数组第一个元素。
			slice();	//从某个数组中提取选定元素：arrayObject.slice(start,end);开始索引，结束位置索引。end可以不写，默认到尾部。
						//索引可以传递负值，表示从后往前：-1：倒数第一个。
			splice();	//删除数组中的指定元素，会影响原数组，并将删除的元素作为返回值返回。并向数组添加新元素。
				//arrayObject.splice(start,num,"xxx","yyy");开始索引，删除的数量,后续参数传递新元素并将其插入至开始位置索引前。
			
			concat();    //连接两个或多个数组并把新数组返回，不会修改原数组。
				//arr1.concat(arr2,arr3,"xxx","yyy");
				
			join();		//将数组转换成一个字符串，不会修改原数组。
						//join()中可以指定一个字符串作为参数，
						//该字符串将会变成数组元素连接符（默认为逗号）.
			reverse();	//反转数组，直接修改原数组。
			sort();		//对数组排序，直接修改原数组，默认按照unicode顺序排序。因此对数字数组可能排序出错，
						//因此可以添加回调函数用于指定排序规则。
						//回调函数中需要两个形参，浏览器分别使用数组中的元素作为实参调用回调函数，
						
				arr.sort(function(a,b){		//a一定在b之前。
					return a - b;			//升序排列
					//浏览器根据回调函数返回值决定元素顺序，大于零则交换位置,等于则相等，小于则不变。
				});

			forEach();	//JS提供的用于遍历数组的方法，只支持IE8及以上的浏览器。
			
				'''js
					arr.forEach(function(value, index, obj){		//需要一个函数作为参数。这种函数由我们创建但不由我们调用叫做回调函数。
						console.log(value);	//数组中有几个元素函数就会执行几次，每次执行时，浏览器会将遍历到的元素以实参形式传递进来，而后可以定义形参，来读取内容。
									//浏览器会在回调函数中传递三个参数：分别是正在遍历的元素，当前元素序列号，和所有的元素。
					});
				'''


			function A(){
				
			}
			function B(a){
				this.a = a;
			}
			function C(a){
				if(a){
					this.a = a;
				}
			}
			A.prototype.a = 1;
			B.prototype.a = 1;
			C.prototype.a = 1;
			
25. 函数对象的方法：call()&apply();		//需要通过函数对象来调用，可以用来修改this
	
		'''js
			function fun(){
				alert("hi!");
			}
			
			fun.apply();	//当对函数调用call()和apply()时，都会调用函数执行
			fun.call();		//在调用这两个函数时可以将一个对象指定为第一个参数
							//此时这个对象将会成为函数执行时的this。
							//call方法可以将实参在对象之后依次传递
							//apply方法应将实参封装到一个数组中统一传递
			fun();
		'''
		
		- this的情况：
			a.以函数形式调用，this指向window；
			b.以方法形式调用，this指向调用方法的对象。
			c.当以构造函数形式调用，this指向新创建的对象。
			d.使用call和apply调用时，this指向指定对象。
		
		- arguments：是一个类数组对象（类似于数组的对象），可以通过索引操作数据获取长度等。
			调用函数时，浏览器传递进两个隐含参数：
				函数上下文对象this；
				封装实参的对象arguments（保存着我们传递的实参）。
			其中有一个属性callee，对应一个函数对象，即当前正在指向的函数对象。
			
26. Date对象（JS中用于表示时间）
		
		'''js
			var d = new Date();		//创建一个Date对象
			console.log(d);			//如果直接使用构造函数创建一个Date()对象，
							//则会封装为当前代码执行的时间.
			//若要创建一个指定的事件对象，需要在构造函数中传递一个表示时间的字符串。
			var d2 = new Date("3/30/2022 11:10:30");	//日期格式： 月/日/年 时：分：秒
		'''
		- 方法
			getDate();	//获取日期
			getDay();	//获取周几（0-6：日-六）
			getMonth();	//获取月份
			getFullYear();	//获取年份
			getTime();	//获取当前日期对象的时间戳（从1970.1.1 0:0:0至当前对象日期的毫秒数）
			Date.now();	//获取执行当前行代码的时间戳，可用于测试性能
			
27. Math：和其他构造函数不同，Math并非一个构造函数，而是一个封装好的工具类，
			无需创建对象，其中封装了数学运算需要的属性和方法。

		- ceil()	//表示向上取整。
		- floor()	//表示向下取整。
		- round()	//表示四舍五入。
		
		- random()	//表示生成一个0-1之间的随机数	0-x：Math.round(Math.random()*x)	
				//x-y：Math.round(Math.random()*(y-x)+x)
		- max(), min()
		- pow(x,y)	//x的y次幂
		
28. 包装类：JS提供了三个包装类，可以将基本数据类型的数据转换为对象，但在实际应用中不使用。

		- String()	//可以将字符串转换为String对象
		- Number()
		- Boolean()
		方法和属性只能添加给对象，不能添加给基本数据类型。当对基本数据类型的值调用属性和方法时，
		浏览器临时使用包装类将其转换成对象，结束后立即销毁，变成基本数据类型。

29. 字符串的方法
		
		- length	//属性，返回字符串长度
		- charAt()	//返回指定位置的字符
		- charCodeAt()	//返回指定位置的字符的Unicode编码
		- fromCharCode()	//根据字符编码获取字符
		- concat();    //连接两个或多个字符串并把新字符串返回，不会修改原字符串。
		- indexof();	//检索一个字符串中是否含有指定内容，有则返回第一次出现的索引，无则-1.
						//可以指定第二个参数，指定开始查找的位置
		- lastIndexof();	//类似上一个，但从后往前。
		- slice();		//可以从字符串中截取指定内容，接受负值。
		- substring();	//类似于slice(),区别在于不接受负值，否则就是0.且会自动交换位置，使小的在前面。
		- substr();		//用于截取字符串，第一个是开始索引，第二个是截取长度。
		- split();		//将一个字符串拆分为一个数组，根据参数字符串（如，‘,’）来拆分。
						//若传递空串则拆分每一个字符。
						//也可传递正则表达式。（本身全局）
		- search();		//也可传递正则表达式。（只会查找第一个）
		- match();		//根据正则表达式，从一个字符串中提取符合条件的内容，封装为数组。
		- replace();	//替换。默认只替换一个。
		- toUpperCase();	//将一个字符串转换为大写并返回。//toLowerCase();
		
30. 正则表达式：用于检查字符串是否符合规则或提取符合规则的内容。

		- 创建正则表达式对象。
			a. 使用构造函数创建（更灵活）
				var reg = new RgeExp("正则表达式"， “匹配模式”);	//typeof为object
					
			b.使用字面量来创建正则表达式	
				var reg = /正则表达式/匹配模式;		//更简单
		
		- 语法：	|		表示或；
					[]		[]里的内容也表示或的关系;	//[a-z]	任意小写字母 [A-Z]	任意大写字母 [A-z]	任意字母
					[^ ]	除了中括号内以外的内容	
					{n}		量词，表示其前一个内容或前一对括号中出现n次
					{x,y}	量词，出现x~y次。
					+		量词，出现至少一次。
					*		量词，出现0个或多个。{0，}
					？		量词，出现0个或1个。{0，1}
					/^a/	检查一个字符串是否以a开头
					/a$	/	检查一个字符串是否以a结尾
					.       表示任意字符
					\.      表示单个.
					\\      表示\

					tips：在使用构造函数时，其参数是字符串，而\在字符串中也是转义字符，因此要使用\则需使用\\。

					\w      表示任意字母数字和下划线 相当于[A-z0-9_]
					\W      表示除了任意字母数字和下划线 相当于[^A-z0-9_]
					\d      表示任意数字 相当于[0-9]
					\D      表示除了数字 相当于[^0-9]
					\s      空格 
					\S      除了空格
					\b      单词边界    
					\B      除了单词边界     
					
					/\bchild\b/ 确保child是个独立单词（即前后都有空格）
					replace(/^\s*｜\s*$/g，“”）匹配开头和结尾的空格并替换为空串

		- 正则表达式方法：
			test();	//可以检查一个字符串是否符合正则表达式的规则。
		- 匹配模式：	i	忽略大小写;		//可以指定多个匹配模式，顺序无所谓。
						g 	全局模式；
						


31. DOM

		全称：document object model，文档对象模型。JS使用dom来对HTML文档进行操作。

		文档：html网页文档；
		对象：将网页中的每个部分转换成对象；
		模型：使用模型来表示对象之间的关系，便于管理。
		节点Node: 构成网页的最基本部分。
		
		-  常用节点
			文档节点：整个HTML文档
			元素节点：HTML标签
			属性节点：元素属性
			文本节点：HTML标签中的文本内容

						nodeName	nodeType	nodeValue
			文档节点	#document	9			null
			元素节点	标签名		1			null
			属性节点	属性名		2			属性值
			文本节点	#text		3			文本内容


		- 浏览器已经提供了文档节点，可以直接使用，即document。
			'''js
			var btn=document.getElementById(“btn”)；//获取button对象
			btn.innerHTML=“I am a button”；//修改按钮文字
			'''
			
		- 事件: 用户和浏览器之间的交互行为（点击、鼠标移动、关闭窗口等），可在事件对应的属性中设置一些js代码，当事件触发时，代码将会执行；但如此耦合过高，不建议。

				可以为按钮的对应事件绑定处理函数的形式来响应事件，当事件触发时，对应的函数被调用。

				单击相应函数：为单击事件绑定的函数。

		- 文档的加载
		
			因为浏览器加载时按照自上向下顺序加载，因此如果script标签写在body之前，代码执行时页面未加载，因此变量为空，为其设置属性则会报错。

			因此，可以使用onload事件，该事件在整个页面加载完成后才出发，为window绑定onload事件，可以确保所有dom对象加载完毕后在执行对应的响应函数。

32. DOM查询
		
		-  获取元素节点

			getElementById();			//通过id获得一组元素节点对象
			getElementsByTagName();		//通过标签名获得一组元素节点对象
			getElementsByName(); 		//通过name属性获取一组元素节点对象

		-  innerHTML
			读取元素内部的html代码，对于自结束标签无意义。
			如需读取元素节点属性，直接使用【元素.属性名】；但class属性不能采用这种方式，读取class 需要使用【元素.className】.
			
		-  innerText
			该属性可以获取到元素内部的文本内容，去除html.

		-  获取元素节点的子节点:通过具体的元素节点调用
			getElementsByTagName();		//方法,返回当前节点的指定标签名后代节点
			childNotes 			//属性，表示当前节点的所有子节点；会获得包括文本节点在内的所有节点（如换行、空白等）。
								//根据DOM标签，标签间空白也是文本节点，ie8及以下浏览器中不会将空白文本当作子节点。
			firstChild 			//属性，表示当前节点的第一个子节点；包括空白文本节点。
			lastChild 			//属性，表示当前节点的最后一个子节点
			children 				//属性，表示当前节点的所有子元素；不会获得空白文本。
			firstElementChild 	//属性，表示当前节点的第一个元素；不会获得空白文本。（不兼容ie8及以下）

		-  获取父节点和兄弟节点
			parentNode; 			//属性
			previousSibling;	//属性（也可能获取空白节点）
			nextSibling; 		//属性
			previousElementSibling;	 //属性，表示获取当前节点的前一个兄弟元素；不会获得空白文本。（不兼容ie8及以下）

		- this
			在事件相应函数中，this绑定与响应函数绑定的对象一致。

		- 引用
			document.body 				//保存对body的引用
			document.document Element	//保存对html的引用
			document.all 				//保存对所有标签的引用，type为undefined。
			getElementByTagName 		//获取同样的标签
			getElementByClassName 		//ie9及以上可用
			document. querySelector() 	//可根据css选择器选择元素对象，ie8及以上可用；但使用该方法只会返回唯一的一个元素，若有多个则只返回第一个元素。
			document. querySelectorAll() 	//类似上一个，但会返回多个并且封装入数组。

		- DOM增删改
			createElement(); 	//创建一个元素节点对象，需要标签名做参数并根据标签名创建元素节点对象，并将创建好的对象返回
			createTextNode(); 	//创建一个文本节点对象，需要文本内容做参数并根据内容创建文本节点对象，并将创建好的节点返回
			appendChild(); 		//向一个父节点中添加一个新的子节点
			insertBefore(); 	//父节点调用,在指定子节点前面插入新的子节点
				//父节点.insertBefore(新节点，旧节点)
			replaceChild();		//替换子节点
				//父节点.replaceChild(新节点，旧节点)
			removeChild();		//删除子节点
				//父节点.removeChild(子节点);	//子节点.parentNode.removeChild(子节点);
			
			tips：使用innerHtml也可以增删改但是动静太大了，可以结合使用。

33. practice
		
		- 添加删除界面
			//点超链接即删除所在行
			超链接点击后会跳转，若想禁止跳转，可以在单击响应函数后return false取消该默认行为。
		- confirm();	//用于弹出一个带有确认和取消按钮的提示框，需要一个字符串做参数，作为提示文字。
				//若选确定返回true，取消返回false。
		- 添加删除记录
		- a的索引问题
			for循环会在页面加载完成时立即执行，响应函数是在超链接点击时执行（因此会带来循环超出限制的问题））
			
33. 使用DOM操作CSS
		
		- 通过js修改元素样式：
			//元素.style.样式名=“样式值”；
			若样式名中含有-，则不合法，需要改为驼峰命名法。
			通过style属性设置的样式都是内联样式，优先级较高，优先显示；
			但如果加入！important,则会有最高优先级，导致js修改样式失效，所以尽量避免！important。
			
		- 通过js获取元素样式：
			//元素.style.样式名;	通过style属性读取的样式也只会是内联样式。
			//元素.currentStyle.样式名		获取元素当前显示的样式（已过时）。
			//getComputedStyle()	window的方法，需要两个参数， 1.需要获取样式的元素，2.伪元素（null）
				//该方法会返回一个对象，封装了当前元素对应的样式。可通过对象.样式名获取到真实值而非默认值。
				//如未设置width则会返回1350px而非auto。但该方法不支持ie8及以下
				/*	正常浏览器：alert(getComputedStyle(box1, null).width);
				/*ie8及以下：alert(box1.currentStyle.width);*/
				
			- tips: 通过currentStyle(), getComputedStyle()获得的元素都是只读的。修改只能通过style。
			- tips： 变量找不到会报错，属性找不到会报undefined。因此在getComputedStyle前面加一个window可以保证不报错。
		
		- 其他样式相关的属性
			clientWidth & clientHeight: 这两个属性可以获取元素的可见宽度和高度，不带px的数字。
				//并且获取的元素宽高包括内容区和内边距，且属性只读，无法修改。只能Style修改。
			offsetWidth & offsetHeight& offsetLeft& offsetTop:	这两个属性可以获取元素的可见宽度和高度，不带px的数字。
				//并且获取的元素宽高包括内容区和内边距和边框，且属性只读，无法修改。只能Style修改。
			offsetParent： 获取当前元素的定位父元素（开启定位的父元素，即定位不是static就可以）。
				//若全无，则返回body。
			offsetLeft & offsetTop: 当前匀速相对于其定位父元素的水平/垂直偏移量。
			scrollWidth  & scrollHeight & scrollLeft& scrollTop:	获取元素整个滚动区域的大小/水平滚动条滚动的距离/垂直滚动条滚动的距离
			
			//tips:当满足scrollHeight-scrollTop==clientHeight,说明垂直滚动条到底，可用于实现阅读协议而后打钩注册效果。
			
		- 练习：滚动条触底注册
			checkBox 和input的submit按钮可以添加disabled属性（true禁用，false可用），当滚动条滚动时使表单项可用。

34. 事件对象
		
			当事件的响应函数被触发时，浏览器每次都将一个事件对象作为实参传递进响应函数（ie8及以下不传递，而是作为window的属性传递）。
		事件对象中封装了一切当前事件相关信息，如鼠标坐标（clientX, clientY），键盘按键，鼠标滚轮滚动方向etc），键盘按键，鼠标滚轮滚动方向etc.
	
		- 练习
			当鼠标在areaDiv中移动时，showMsg中显示鼠标坐标。
			
			- onmousemove：该事件会在鼠标在元素中移动时被触发。
			
			- // clientX和Y表示的是鼠标在可见窗口的坐标，而div偏移针对于整个页面，因此下滑会出现距离。
			  //而pageX和Y表示的是整个页面的鼠标坐标,但在ie8中不支持。(因此可以使用scrollTop+clientY给div赋值。)
			- 获取全局滚动条:chrome认为浏览器滚动条是body的，可以由body.scrollTop获取；
							 火狐等认为是html的，需要由documentElement.scrollTop获取。
		
		- 事件冒泡（Bubble）
			所谓冒泡指事件向上传导，当后代元素上的事件被触发时，其祖先元素的相同事件也会被触发。
			
			开发中，大部分冒泡都是有用的，如果不希望发生事件冒泡，可以通过事件对象来取消冒泡。
			
			event.cancelBubble = true;	//取消冒泡。
			
		- 事件委派
		
			case:为每个超链接都绑定单机响应函数，但若创建新的，则没有单机响应函数。
			需求：希望只绑定一次事件即可应用到多个元素上，即使是后添加元素，可以将其绑定给共同的祖先元素。
			
			
			事件委派：指将事件统一绑定给共同祖先元素，当后代元素上的事件触发时，会冒泡至祖先元素，从而利用祖先的响应函数来解决问题。
					利用了冒泡，可以减少事件绑定次数，提高程序性能。
			
			实现：如果触发事件对象是我们期望的元素则执行，否则不执行。->event.target.className =="xxx";
		
		- 事件绑定
			case:使用 对象.事件 = 函数 形式绑定响应函数，同时只能为一个元素的一个事件绑定一个函数
				若绑定多个后边的会覆盖。
			实现：addEventListener()：为元素绑定函数，一个事件，多个响应函数（时间顺序触发）。
					/*参数：1.事件的字符串删掉on。（“click”）；
					*		2.回调函数，事件触发时该函数被调用；
					*		3.是否在捕获阶段触发事件，false（布尔值）；
					* tip:this指绑定事件对象
					*缺陷： ie8及以下不支持。
					/
				  attachEvent():同上，后绑定先执行，即顺序相反；支持ie8。
					/*参数：1.事件的字符串要on。（“onclick”）；
					*		2.回调函数
					*tip:this指window
					*/
				具体兼容性实现：定义一个函数，用于为指定元素绑定响应函数。
					//tip：需要统一两种方法的this。
					//this由调用方式决定，callback由浏览器调用，可以通过先调用匿名函数，
					//通过匿名函数调用callback（此时并非浏览器调用）， 修改callback.call(obj)修改this指向。
		- 事件传播
			背景：微软认为事件传播应由内向外传播（类似冒泡，先触发孩子后触发祖先）；
					网景认为事件传播由外向内传，与上相反（捕获思路）。
					W3C综合以上，将事件传播分为三个阶段：
						1.捕获阶段（从外向内捕获）
						2.目标阶段（执行）
						3.冒泡阶段（从内向外执行）
					若希望在捕获阶段触发事件，可将addEventListener第三个参数设置为true。
					
					ie8及以下没有捕获阶段。
		
35. 练习：拖拽

		- 流程：
			1.鼠标在拖拽元素上按下时，开始拖拽	onmousedown
			2.鼠标移动时，被拖拽元素跟随鼠标移动 onmousemove
			3.鼠标松开时，被拖拽元素固定在当前位置 onmouseup
		
		- 新的问题
			当选中文字并拖拽网页内容时，浏览器默认搜索内容，此时会导致拖拽功能异常，这是浏览器提供的默认功能。
			
			解决：1.return false(ie8不起作用).
				  2.setCapture()(仅兼容ie8)
					当调用一个元素的setCapture()事件时，下一次鼠标的点击相关事件都被捕获到该元素自身上。
					因此可以当点击入box1中，设置box1捕获所有鼠标操作，并在鼠标松开时，取消事件捕获（releaseCapture()）。

36. 练习：鼠标滚轮事件
		
		- 流程：
			鼠标滚轮向下滚动，box1变长；向上滚动反之。
			onmousewheel，鼠标滚轮滚动。
			event.wheelDelta 滚动方向。下负上正。
		- 新的问题
			onmousewheel在火狐中不支持，需要使用DOMMouseScroll来绑定事件，注意需要通过addEventListener()来添加绑定事件。
			wheelDelta在火狐中不支持，需要使用event.detail.上负下正。
			
			当滚轮滚动时，若浏览器有滚动条，滚动条随之滚动，默认行为。
			若想取消则return false取消该默认行为。
			
			对通过addEventListener()绑定的事件需要使用event来取消(但ie8不支持)。
			event.preventDefault();
			
37. 键盘事件
		
		onkeydown 	按键被按下，若一直按着某个按键不松手，事件会一直触发。
					连续触发时，在第一次和第二次连续触发间会有一个长间隔。（防止误操作）
		onkeyup 	按键被松开

		键盘事件一般绑定给可以获取到焦点的对象或document。

		event.keyCode：获取按键的编码。可以判断哪个按键被按下。
		
		event.altKey 
		event.ctrlKey
		event.shiftKey
			这三个用来判断alt ctrl 和shift是否被按下，如果按下则返回true，否则返回false.


		在文本框中输入内容属于onkeydown的默认行为，若return false取消默认行为，则输入内容无法写入文本框。


38. BOM

		一种浏览器对象模型，使用户通过JS操作浏览器。BOM中提供一组对象用于完成对浏览器的操作。
		
		BOM对象
		- window
			代表整个浏览器的窗口，同时也是网页中的全局对象。
		- 定时器相关
			定时调用：
				setInterval（）：定时调用，作用于需要程序间隔执行的场景。
					参数：1.回调函数，每隔一段时间执行一次；2.每次调用间隔时间（毫秒）
					返回值：number类型数据，用于唯一标识该定时器。
				clearInterval（timer）：用于关闭定时器，可以接受任意参数，若参数有效则停止对应定时器，若无效则不操作。

			缺陷：每单击一次都会开一个定时器，则加速定时器，并且关闭只能关闭最后一个定时器。
			解决：开启一个定时器之前先关闭当前元素的其他定时器。

			延时调用：
				setTimeOut（）：隔一段时间之后执行，且只执行一次。如调用广告关闭的场景。
				clearTimeOut（）：关闭延时调用。
			
			定时调用和延时调用可以互相代替。
		
		- Navigator
			代表当前浏览器的信息，用于识别不同的浏览器。一般使用userAgent属性来判断浏览器信息（其他大部分已经过期），
			但在ie11中已经将msie标识去除，无法识别。即可以通过ie独有对象来判断（activeXObject()）。

			if(“activeXObject” in window){};

		- Location
			代表浏览器地址栏信息，用于获取地址栏或操作跳转页面。
			若修改location则会直接跳转并生成历史记录。
			方法：
				assign（）：用于直接跳转，类似于修改location。
				reload（）：重新加载当前页面，类似f5（但不清空缓存，若想强制清空可以ctrl+f5，或在方法中传入true）。
				replace（）：使用新页面替换当前页面，调用完毕也会跳转页面，但不会生成历史记录，无法回退。
			
		- History
			代表浏览器历史记录，由于隐私，无法获取具体历史记录，只能前后翻页，且只在当次访问时有效。
			
			属性：length 返回当前访问链接的数量。
			方法：	back（）&forward（）回退与前进。
					go（）：跳转至指定页面，需要参数，指定向前（正）或向后（负）跳转几个页面。

		 - Screen
			代表用户屏幕信息，但主要使用在移动端而非pc端。

		这些BOM对象都作为window对象的属性保存，可作为window对象使用或直接使用。


39. 练习：
	
		定时器:
			div奔跑
			缺陷：定时器为全局应用，导致黄块跑的时候关闭了红块的定时器。
			解决：向执行动画的对象中添加一个timer属性，用于保存自己定时器的标志。

		轮播图
			tips：setA和获取超链接索引。
		
		二级菜单折叠
			要点：过渡效果变化时，切换高度前后各记录一次，切换后赋内联样式初值并做出切换效果，最后修改内联样式。


40. 类的操作

		问题：通过style属性修改元素样式效率差，每修改一个样式就需要重新渲染一次页面，性能低。
		解决：可以修改元素的className，间接修改样式。浏览器只需重新渲染页面一次，性能变高，且耦合程度更低。

		box.className += “ b2”；

		问题：检查类中是否有某一类.
		解决：创建正则表达式检测。

		var reg = new RegExp(“\\b”+cn+ “\\b”);
		Return reg.test(obj.className);

		ToggleClass:用于切换一个类，有则删除，无则添加。

41. JSON（javascript object notation js对象表示法）
		一种特殊格式的字符串，用于交互数据（前后端）的通用语言格式。可被任意语言识别并转换。

		语法：属性名必加双引号。
		分类：对象｛｝，数组[].
		允许的值：字符串 对象 数组 数值 布尔值 null

		- JSON转JS对象
			JSON工具类：可用于互相转换
			JSON.parse（）：json字符串转js对象。
			JSON.stringify（）：js对象转json字符串。

		- 兼容性问题：JSON在ie7及以下不支持。
			解决方式：
			1.eval（）：用于执行字符串形式的js代码，会把｛｝当成是代码块，为防止误识别应该在str外侧加上括号“（”“）”；太强大别用了。
			2.引入外部js文件。