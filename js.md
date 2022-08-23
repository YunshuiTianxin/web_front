# js基础 #
# js的遍历 定时器任务 还有正则请自行整理 #
## 1.JavaScript 简介 ##
	JavaScript是一种直译式脚本语言，是一种动态类型、弱类型、基于原型的语言，内置支持类型。
	它的解释器被称为JavaScript引擎，为浏览器的一部分，广泛用于客户端的脚本语言，
	最早是在HTML（标准通用标记语言下的一个应用）网页上使用，用来给HTML网页增加动态功能。
## 2.<script\> 标签 ##
	1. 在 HTML 页面中插入 JavaScript，使用 <script></script> 标签。
	2. <script> 和 </script> 表示 JavaScript 的开始和结束。
	3. 可以在 HTML 文档中放入不限数量的脚本。
	4. 脚本可位于 HTML 的 <body> 或 <head> 部分中，或者同时存在于两个部分中。
	3. 建议写在</body>的后面,不会干扰页面的内容。
	
	示例:
	<script>
		alert("我的第一个 JavaScript");
	</script>
	浏览器会解释并执行位于 <script> 和 </script>之间的 JavaScript 代码
## 3.JavaScript的三种使用方式 ##
### 3.1.直接和html代码写在一起 ###
	<body>	
		<button onclick="javascript:alert('我被点击了')">点击按钮</button>
	</body>
	1. onclick是元素的点击事件
	2. javascript:alert('我被点击了') 是点击事件触发的js代码

### 3.2.写在html文档中的script标签里 ###
	<body>
		<button onclick="f()">点击按钮</button>
	</body>
	<script>
		function f(){
			alert("我被点击了");
		}
	</script>
	
	1. function 表示定义一个函数
	2. f() 是函数的名字,函数后面必须跟()
	3. onclick="f()" 表示当按钮被点击后调用f()这个函数
### 3.3.写在外部的js文件里,再引入到html文档中 ###
1. 在html中引入first.js文件

![image](https://note.youdao.com/yws/res/2126/95C1B3CC19084B80AD5F39687DC3592E)

2. first.js文件中的代码

![image](https://note.youdao.com/yws/res/2127/7A688407331346CE8F2DEDD7221C4DBD)

## 4. JavaScript语法 ##
### 4.1.字面量 ###

在编程语言中，一般固定值称为字面量，如 3.14。

数字（Number）字面量 可以是整数或者是小数，或者是科学计数(e)。

	3.14
	
	1001
	
	123e5

字符串（String）字面量 可以使用单引号或双引号:

	"John Doe"
	
	'John Doe'

表达式字面量 用于计算：

	5 + 6
	
	5 * 10
数组（Array）字面量 定义一个数组：

	[40, 100, 1, 5, 25, 10]

对象（Object）字面量 定义一个对象：

	{firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"}

函数（Function）字面量 定义一个函数：

	function myFunction(a, b) { return a * b;}
### 4.2.变量 ###

JavaScript 使用关键字 var 来定义变量， 使用等号来为变量赋值：
	var length=50;

	var x,y;
	
	x = 5;
	
	y = 6;
### 4.3.数据类型 ###

值类型(基本类型)：

	1. 字符串（String）
	2. 数字(Number)
	3. 布尔(Boolean)
	4. 空（Null）
	5. 未定义（Undefined）
	6. Symbol
		注:Symbol是es6引入的新类型,表示独一无二的值

引用数据类型：

	1. 对象(Object)
	2. 数组(Array)
	3. 函数(Function)

JavaScript 拥有动态类型
这意味着相同的变量可用作不同的类型：

	var x;               // x 为 undefined
	x = 5;           	 // 现在 x 为数字
	x = "John";          // 现在 x 为字符串

Undefined 和 Null

	null 和 undefined 都表示"值的空缺"
	
	null： Null类型，代表“空值”，代表一个空对象指针，使用typeof运算得到 “object”，所以你可以认为它是一个特殊的对象值。
	
	undefined： Undefined类型，当一个声明了一个变量未初始化时，得到的就是undefined。

### 4.4.运算符 ###

1. 赋值运算符 =
	
	运算符 = 用于给 JavaScript 变量赋值。

2. 运算符 + 
	
	运算符 + 有两种含义:
	1. 表达式为数字,做加法运算
	2. 表达式为字符串,做连接运算

3. 算术运算符

![image](https://note.youdao.com/yws/res/2130/FD0DD652F5AC473D94FC902295F8EDC5)

4. 比较运算符

![image](https://note.youdao.com/yws/res/2133/E9DB4CFB7E0F43C4878CF9E2338E8AA6)

5. 逻辑运算符

![image](https://note.youdao.com/yws/res/2136/D50BAE6B2B544EC1960694B1E461F634)

6. 三元运算符 ?

	var score = 58;
	var result = score>60?"考核通过":"考核失败"

### 4.5.注释 ###
	单行注释,使用 //
	多行注释,使用 /**/

### 4.6.函数 ###

函数就是包裹在花括号中的代码块，前面使用了关键词 function 声明

	function name()
	{
	    var a=3;
		var b=5;
		console.log(a*b);
	}
### 4.7.带参数的函数 ###

	function name(a,b)
	{
		console.log(a*b);
	}

### 带返回值的函数 ###

	function name(a,b)
	{
		return a*b;
	}

### 4.8.作用域和生命周期 ###
局部作用域

函数内声明的变量称为局部变量,只能在函数内部访问。

	// 函数外不能使用 carName 变量
	function myFunction() {
	    var carName = "Volvo";
	    // 函数内可使用 carName 变量
	}

变量生命周期

JavaScript 变量生命周期在它声明时初始化。

局部变量在函数执行完毕后销毁。

全局变量在页面关闭后销毁。

函数的参数属于局部变量


### 4.9.事件 ###

HTML 事件可以是浏览器行为，也可以是用户行为。

常见的HTML事件

![web12.png](https://note.youdao.com/yws/res/2845/WEBRESOURCEf31f8abfff94417af3d4b258b7ccaf62)


### 4.10.字符串 ###
字符串属性:

	length 返回字符串长度

字符串函数:

![image](https://note.youdao.com/yws/res/2141/6D066F3AC407400BB1F6507F22B8CFE3)
### 4.16.typeof ###

使用 typeof 操作符来检测变量的数据类型。

	typeof "John"                // 返回 string 
	typeof 3.14                  // 返回 number
	typeof false                 // 返回 boolean
	typeof [1,2,3,4]             // 返回 object
	typeof {name:'John', age:34} // 返回 object
### 4.17.类型转换 ###

1、直接转换 parseInt() 与 parseFloat()

```
alert('12'+7); //弹出127
alert( parseInt('12') + 7 );  //弹出19 
alert( parseInt(5.6));  // 弹出5
alert('5.6'+2.3);  // 弹出5.62.3
alert(parseFloat('5.6')+2.3);  // 弹出7.8999999999999995
alert(0.1+0.2); //弹出 0.3000000000000004
alert((0.1*100+0.2*100)/100); //弹出0.3
alert((parseFloat('5.6')*100+2.3*100)/100); //弹出7.9
```

2、隐式转换 “==” 和 “-”

```
if('3'==3)
{
    alert('相等');
}

// 弹出'相等'
alert('10'-3);  // 弹出7
```

3、NaN 和 isNaN

```
alert( parseInt('123abc') );  // 弹出123
alert( parseInt('abc123') );  // 弹出NaN
```

​	

### 4.19.调试 ###

在程序代码中寻找错误叫做代码调试。

调试很难，但幸运的是，很多浏览器都内置了调试工具。

内置的调试工具可以开始或关闭，严重的错误信息会发送给用户。

有了调试工具，我们就可以设置断点 (代码停止执行的位置), 且可以在代码执行时检测变量。

浏览器启用调试工具一般是按下 F12 键，并在调试菜单中选择 "Console" 。

console.log() 方法

	a = 5;
	b = 6;
	c = a + b;
	console.log(c);

设置断点

	在调试窗口中，你可以设置 JavaScript 代码的断点。
	
	在每个断点上，都会停止执行 JavaScript 代码，以便于我们检查 JavaScript 变量的值。
	
	在检查完毕后，可以重新执行代码（如播放按钮）。

### 4.20.变量提升 ###
JavaScript 中，函数及变量的声明都将被提升到函数的最顶部。

JavaScript 中，变量可以在使用后声明，也就是变量可以先使用再声明。

以下两个示例将获得相同的结果：
	
示例1:
	

	x = 5; // 变量 x 设置为 5
	
	elem = document.getElementById("demo"); // 查找元素 
	elem.innerHTML = x;                     // 在元素中显示 x
	
	var x; // 声明 x

示例2:

	var x; // 声明 x
	x = 5; // 变量 x 设置为 5
	
	elem = document.getElementById("demo"); // 查找元素 
	elem.innerHTML = x;                     // 在元素中显示 x

要理解以上实例就需要理解 "hoisting(变量提升)"。

变量提升：函数声明和变量声明总是会被解释器悄悄地被"提升"到方法体的最顶部。

初始化的变量不会提升
JavaScript 只有声明的变量会提升，初始化的不会。

以下两个示例结果结果不相同：

示例1:

	var x = 5; // 初始化 x
	var y = 7; // 初始化 y
	
	elem = document.getElementById("demo"); // 查找元素 
	elem.innerHTML = x + " " + y;           // 显示 x 和 y

示例2:

	var x = 5; // 初始化 x
	
	elem = document.getElementById("demo"); // 查找元素 
	elem.innerHTML = x + " " + y;           // 显示 x 和 y
	
	var y = 7; // 初始化 y

示例 2 的 y 输出了 undefined，这是因为变量声明 (var y) 提升了，但是初始化(y = 7) 并不会提升，所以 y 变量是一个未定义的变量。

示例 2 类似以下代码:

	var x = 5; // 初始化 x
	var y;     // 声明 y
	
	elem = document.getElementById("demo"); // 查找元素
	elem.innerHTML = x + " " + y;           // 显示 x 和 y
	
	y = 7;    // 设置 y 为 7


### 4.21.严格模式(use strict) ###

使用 "use strict" 指令
"use strict" 指令在 es5 (ECMAScript5) 中新增。

它不是一条语句，但是是一个字面量表达式，在 JavaScript 旧版本中会被忽略。

"use strict" 的目的是指定代码在严格条件下执行。

严格模式下你不能使用未声明的变量。

示例:

	"use strict";
	x = 3.14;       // 报错 (x 未定义)

示例:

	"use strict";
	myFunction();
	
	function myFunction() {
	    y = 3.14;   // 报错 (y 未定义)
	}
### 4.22.常见使用误区 ###
### 4.23.this 关键字 ###

面向对象语言中 this 表示当前对象的一个引用。

但在 JavaScript 中 this 不是固定不变的，它会随着执行环境的改变而改变。

在方法中，this 表示该方法所属的对象。

如果单独使用，this 表示全局对象。

在函数中，this 表示全局对象。

在函数中，在严格模式下，this 是未定义的(undefined)。

在事件中，this 表示接收事件的元素。

### 4.24.let 和 const ###

ES2015(ES6) 新增加了两个重要的 JavaScript 关键字: let 和 const。

let 声明的变量只在 let 命令所在的代码块内有效。

const 声明一个只读的常量，一旦声明，常量的值就不能改变。

在 ES6 之前，JavaScript 只有两种作用域： 全局变量 与 函数内的局部变量。

全局变量

	var carName = "Volvo";
	 
	// 这里可以使用 carName 变量
	 
	function myFunction() {
	    // 这里也可以使用 carName 变量
	}

全局变量在 JavaScript 程序的任何地方都可以访问。

局部变量

在函数内声明的变量作用域是局部的（函数内）：

	// 这里不能使用 carName 变量
	function myFunction() {
	    var carName = "Volvo";
	    // 这里可以使用 carName 变量
	} 
	// 这里不能使用 carName 变量

函数内使用 var 声明的变量只能在函数内容访问，如果不使用 var 则是全局变量。

ES6后新增:块级作用域(Block Scope)

使用 var 关键字声明的变量不具备块级作用域的特性，它在 {} 外依然能被访问到。

	{ 
	    var x = 2; 
	}
	// 这里可以使用 x 变量
	
	在 ES6 之前，是没有块级作用域的概念的。
	
	ES6 可以使用 let 关键字来实现块级作用域。
	
	let 声明的变量只在 let 命令所在的代码块 {} 内有效，在 {} 之外不能访问。
	
	{ 
	    let x = 2;
	}
	// 这里不能使用 x 变量

重新定义变量

使用 var 关键字重新声明变量可能会带来问题。

在块中重新声明变量也会重新声明块外的变量：

	var x = 10;
	// 这里输出 x 为 10
	{ 
	    var x = 2;
	    // 这里输出 x 为 2
	}
	// 这里输出 x 为 2

let 关键字就可以解决这个问题，因为它只在 let 命令所在的代码块 {} 内有效。

	var x = 10;
	// 这里输出 x 为 10
	{ 
	    let x = 2;
	    // 这里输出 x 为 2
	}
	// 这里输出 x 为 10

循环作用域

使用var 关键字，它声明的变量是全局的，包括循环体内与循环体外。

	var i = 5;
	for (var i = 0; i < 10; i++) {
	    // 一些代码...
	}
	// 这里输出 i 为 10

使用 let 关键字， 它声明的变量作用域只在循环体内，循环体外的变量不受影响。

	let i = 5;
	for (let i = 0; i < 10; i++) {
	    // 一些代码...
	}
	// 这里输出 i 为 5


const 关键字

const 用于声明一个或多个常量，声明时必须进行初始化，且初始化后值不可再修改：

	const PI = 3.141592653589793;
	PI = 3.14;      // 报错
	PI = PI + 10;   // 报错

const和let 相同点：

二者都是块级作用域

都不能和它所在作用域内的其他变量或函数拥有相同的名称

const和let 不同点：

const声明的常量必须初始化，而let声明的变量不用

const 定义常量的值不能通过再赋值修改，也不能再次声明。而 let 定义的变量值可以修改。

### 4.25.javascript:void(0) ###
下面的代码创建了一个超链接，当用户点击以后不会发生任何事。

	<a href="javascript:void(0)">单击此处什么也不会发生</a>

当用户链接时，void(0) 计算为 0，但 Javascript 上没有任何效果。

### 4.26.href="#"与href="javascript:void(0)"的区别 ###

\# 包含了一个位置信息，默认的锚是#top 也就是网页的上端。

而javascript:void(0), 仅仅表示一个死链接。

在页面很长的时候会使用 # 来定位页面的具体位置，格式为：# + id。

如果你要定义一个死链接请使用 javascript:void(0) 。



### 4.29.Array 数组 ###

创建数组, 为其赋值：

	var mycars = new Array();
	mycars[0] = "Saab";
	mycars[1] = "Volvo";
	mycars[2] = "BMW";

创建数组有三种方法。

1: 使用无参Array构造方法:

	var myCars=new Array(); 
	myCars[0]="Saab";       
	myCars[1]="Volvo";
	myCars[2]="BMW";

2: 使用有参Array构造方法:

	var myCars=new Array("Saab","Volvo","BMW");

3: 字面量:

	var myCars=["Saab","Volvo","BMW"];




### 4.31.获取元素方法

可以使用内置对象document上的getElementById方法来获取页面上设置了id属性的元素，获取到的是一个html对象，然后将它赋值给一个变量，比如：

```
<script type="text/javascript">
    var oDiv = document.getElementById('div1');
</script>
....
<div id="div1">这是一个div元素</div>
```

上面的语句，如果把javascript写在元素的上面，就会出错，因为页面上从上往下加载执行的，javascript去页面上获取元素div1的时候，元素div1还没有加载，解决方法有两种：

第一种方法：将javascript放到页面最下边

```
....
<div id="div1">这是一个div元素</div>
....

<script type="text/javascript">
    var oDiv = document.getElementById('div1');
</script>
</body>
```

第二种方法：将javascript语句放到window.onload触发的函数里面,获取元素的语句会在页面加载完后才执行，就不会出错了。

```
<script type="text/javascript">
    window.onload = function(){
        var oDiv = document.getElementById('div1');
    }
</script>

....

<div id="div1">这是一个div元素</div>
```

### 4.32.操作元素属性

获取的页面元素，就可以对页面元素的属性进行操作，属性的操作包括属性的读和写。

**操作属性的方法** 
1、“.” 操作
2、“[ ]”操作

**属性写法**

1、html的属性和js里面属性写法一样
2、“class” 属性写成 “className”
3、“style” 属性里面的属性，有横杠的改成驼峰式，比如：“font-size”，改成”style.fontSize”

通过“.”操作属性：

```
<script type="text/javascript">

    window.onload = function(){
        var oInput = document.getElementById('input1');
        var oA = document.getElementById('link1');
        // 读取属性值
        var val = oInput.value;
        var typ = oInput.type;
        var nam = oInput.name;
        var links = oA.href;
        // 写(设置)属性
        oA.style.color = 'red';
        oA.style.fontSize = val;
    }

</script>

......

<input type="text" name="setsize" id="input1" value="20px">
<a href="https://www.baidu.com" id="link1">iweb</a>
```

通过“[ ]”操作属性：

```
<script type="text/javascript">

    window.onload = function(){
        var oInput1 = document.getElementById('input1');
        var oInput2 = document.getElementById('input2');
        var oA = document.getElementById('link1');
        // 读取属性
        var val1 = oInput1.value;
        var val2 = oInput2.value;
        // 写(设置)属性
        // oA.style.val1 = val2; 没反应
        oA.style[val1] = val2;        
    }

</script>

......

<input type="text" name="setattr" id="input1" value="fontSize">
<input type="text" name="setnum" id="input2" value="30px">
<a href="https://www.baidu.com" id="link1">iweb</a>
```

**innerHTML** 
innerHTML可以读取或者写入标签包裹的内容

```
<script type="text/javascript">
    window.onload = function(){
        var oDiv = document.getElementById('div1');
        //读取
        var txt = oDiv.innerHTML;
        alert(txt);
        //写入
        oDiv.innerHTML = '<a href="https://www.baidu.com">iweb<a/>';
    }
</script>

......

<div id="div1">这是一个div元素</div>
```



