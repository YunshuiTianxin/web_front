# web前端-chapt02 #

## 1.CSS简介 ##
	CSS 指层叠样式表 (Cascading Style Sheets)
	1. 样式定义如何显示 HTML 元素
	2. 样式通常存储在样式表中
	3. 内容与表现分离
	4. 外部样式表可以极大提高工作效率
	5. 外部样式表通常存储在 CSS 文件中
	6. 多个样式定义可层叠为一个
## 2.CSS语法 ##
![image](https://note.youdao.com/yws/res/2504/C15C0DC17F564B4196210B7E6A56C5E7)

	1. 选择器:表示选中某一个元素或某一类元素
	2. 属性和值为一组申明,设置该元素的某个属性的取值
	3. 用{}包裹申明,用;分隔申明

## 3.CSS选择器 ##
### 3.1.基本选择器 ###

一段html代码

	<div>
		<form>
			<input type="text"placeholder="用户名/手机/邮箱"/>
			<input type="password"placeholder="请输入密码"/>
			<input type="button" value="登录" />
		</form>
	</div>

#### 3.1.1. 标签选择器

	选择器的名字为标签名,表示所有的同类标签受影响
	
	示例：
	input{
		width: 200px;
		height: 30px;
		margin: 5px;
	}
	表示所有的input标签受影响
#### 3.1.2. 类选择器

​	

	选择器的名字为自定义的类名,命名格式为".className"
	
	示例:
	.c1{
		padding-left: 10px;
	}
	
	<input type="text" class="c1" placeholder="用户名/手机/邮箱"/>
	<input type="text" class="c1" placeholder="请输入密码"/>
	
	1. .c1 是类选择器名称
	2. class="c1" 表示该标签受.c1样式的影响
	3. 类选择器可以重复使用
	4. 类选择器可以用于任意标签

#### 3.1.3. ID选择器

	选择器的名称为自定义的ID,命名格式为"#ID"
	
	示例:
	#login-box{
		display: flex;
		width: 250px;
		height: 200px;
		border: 1px solid #999;
		border-radius: 10px;
		text-align: center;
		align-items: center;
	}
	#login-btn{
		border: none;
		text-align: center;
		background-color: skyblue;
		color: white;
	}
	
	<div id="login-box">
	
	<input type="button" id="login-btn" value="登录" />
	
	1. #login-box和#login-btn 是ID选择器的名称
	2. id="login-btn" 表示该标签受#login-btn样式的影响
	3. ID选择器只能使用一次
	4. ID选择器可以用于任意标签


### 3.2.层次选择器 ###
	<div id="box">
		<p  class="active">p1</p>
		<!-- 为了说明相邻兄弟选择器，在此处添加一个类名active -->
		<p>p2</p>
		<p>p3</p>
		<ul>
			<li>
				<p>p4</p>
			</li>
			<li>
				<p>p5</p>
			</li>
			<li>
				<p>p6</p>
			</li>
		</ul>
	</div>

#### 3.2.1.后代选择器

	#box p{
		background: red;
	}
	
	1. #box p 表示选中所有#box的后代p元素,p1-p6都会被选中

#### 3.2.2.子选择器

	#box>p{
		background: pink;
	}
	
	1. #box>p 表示选中所有#box的子级p元素,p1-p3会被选中

#### 3.2.3.相邻兄弟选择器

	.active + p{
		background: green;
	}
	
	1. .active + p 表示选中.active元素的下一个相邻的p元素,p2会被选中

#### 3.2.4.通用兄弟选择器

	.active~p{
		background: yellow;
	}
	
	1. .active~p 表示选中.active元素后面的所有同级p元素,p2-p3会被选中


### 3.3.伪类选择器 ###

一段html 代码
```
	<h2>结构伪类选择器</h2>
	<p>p1</p>
	<p>p2</p>
	<p>p3</p>
	<ul>
		<li>li1</li>
		<li>li2</li>
		<li>li3</li>
	</ul>
```
#### 3.3.1. first-child 

选中第一个子元素

	ul li:first-child{
		background: red;
	}

#### 3.3.2. last-child 

选中最后一个子元素

	ul li:last-child{
		background: green;
	}

#### 3.3.3. E:nth-child(n) 

	ul li:nth-child(2){
		background: yellow;
	}
	
	* 此处n 为odd表示选中所有奇数项
	* 此处n 为even表示选中所有偶数项
	* odd和even可用于隔行变色效果

#### 3.3.4. E:nth-of-type(n) 

	p:nth-of-type(2){
		background: blue;
	}

### 3.4.属性选择器 ###

一段html和css代码
	
	a {
	    display: inline-block;
	    height: 50px;
	    width: 50px;
	    border-radius: 10px;
	    text-align: center;
	    background: #aac;
	    color: blue;
	    font: bold 20px/50px Arial;
	    text-decoration: none;
	    margin: 5px;
	} 
	
```	
	<div>
	    <a href="http://www.baidu.com" class="links item first" id="first" >1</a>
	    <a href="" class="links active item" title="test website" target="_blank" >2</a>
	    <a href="sites/file/test.html" class="links item"  >3</a>
	    <a href="sites/file/test.png" class="links item" > 4</a>
	    <a href="sites/file/image.jpg" class="links item" >5</a>
	    <a href="efc" class="links item" title="website link" >6</a>
	    <a href="/a.pdf" class="links item" >7</a>
	    <a href="/abc.pdf" class="links" >8</a>
	    <a href="abcdef.doc" class="links item" >9</a>
	    <a href="abd.doc" class="linksitem last" id="last">10</a>
	</div>
```

3.4.1. 选中存在属性id的元素

	a[id] {
	    background: yellow;
	}

3.4.2. 选中属性class="links"的元素

	a[class="links"] {
	    background: red;
	}

3.4.3. 选中属性class里包含links字符串的元素

	a[class*=links] {
	    background: red;
	}

3.4.4. 选中属性href里以http开头的元素

	a[href^=http] {
	    background: red;
	}

3.4.5. 选中属性href里以png结尾的元素

	a[href$=png] {
	    background: red;
	}

## 4.添加CSS样式的三种方式 ##
### 4.1.外部样式表(External style sheet) ###
	css 代码写在外部css文件中,然后在html中引入css文件
	引入方式有两种:link 和 import
	
	1. link 引入语法
		<link rel="stylesheet" href="xx.css">
	2. @import 引入语法
		<style type="text/css">
	        @import url("xx.css");
	    </style>
	
	区别:
	1. 加载页面时，link标签引入的 CSS 被同时加载
	2. @import引入的 CSS 将在页面加载完毕后被加载
	3. 如果页面内容多,@import 引入css可能会出现片刻页面没有样式,用户体验不好,因此推荐使用link引入

### 4.2.内部样式表(Internal style sheet) ###
	css代码写在html文件中的<style></style>标签内
	
	示例:
	<style>
		h1{
			color:red;
		}
	</style>
### 4.3.行内样式(Inline style) ###
	css代码和html代码写在一行,使用style属性
	
	示例:
	<h1 style="color:red">家用电器</h1>

## 5.CSS属性 ##
### 5.1.文本 ###
5.1.1. color 文本颜色

	取值：
	1. 十六进制颜色码,如:#fff
	2. 颜色的英文名称,如:red
	3. 红绿蓝三原色rgb函数,如:rgb(255,255,225)
	4. 红绿蓝三原色加透明度rgba()函数,如:rgba(255,255,255.0.5)

5.1.2. text-align 文本对齐方式
	取值:
	1. center 文本居中
	2. right 靠右对齐
	3. left 靠左对齐

5.1.3. text-decoration 文本装饰线

	取值:
	1. underline 有下划线
	2. overline 有上划线
	3. line-through 有删除线
	4. none 没有线

5.1.4. line-height 设置行高

### 5.2.字体 ###

5.2.1. font-family 字体类型

5.2.2. font-size 字体大小

5.2.3. font-weight 字体粗细

5.2.4. font-style 字体风格

5.2.5. 四合一写法 font:风格 粗细 大小 类型

### 5.3.背景 ###

5.3.1. background-color 背景颜色

5.3.2. background-image 背景图片

5.3.3. background-position 背景定位

5.3.4. background-repeat 背景重复

5.3.5. background-size 背景图片大小

5.3.6. background-attachment 背景图片固定

5.3.7. 四合一写法 background:颜色 图片 重复 定位

### 5.4.链接 ###

5.4.1. a:link  未访问链接 

5.4.2. a:visited 已访问链接

5.4.3. a:hover 鼠标悬浮到链接上

5.4.4. a:active 鼠标点击时

注意: hover必须在:link和 a:visited之后定义才有效.

注意:active必须在hover之后定义是有效的

### 5.5.列表 ###

5.5.1. 去除无序列表的黑点和有序列表的序号

	list-style:none

### 5.6.盒子模型 ###

元素在页面中显示成一个方块，类似一个盒子，CSS盒子模型就是使用现实中盒子来做比喻，帮助我们设置元素对应的样式。盒子模型示意图如下：

![](images\box01.png)

把元素叫做盒子，设置对应的样式分别为：盒子的边框(border)、盒子内的内容和边框之间的间距(padding)、盒子与盒子之间的间距(margin)。

**设置边框** 
设置一边的边框，比如顶部边框，可以按如下设置：

```
border-top-color:red;    /* 设置顶部边框颜色为红色 */  
border-top-width:10px;   /* 设置顶部边框粗细为10px */   
border-top-style:solid;  /* 设置顶部边框的线性为实线，常用的有：solid(实线)  
  dashed(虚线)  dotted(点线); */
```

上面三句可以简写成一句：

```
border-top:10px solid red;
```

设置其它三个边的方法和上面一样，把上面的'top'换成'left'就是设置左边，换成'right'就是设置右边，换成'bottom'就是设置底边。

四个边如果设置一样，可以将四个边的设置合并成一句：

```
border:10px solid red;
```

**设置内间距padding**

设置盒子四边的内间距，可设置如下：

```
padding-top：20px;     /* 设置顶部内间距20px */ 
padding-left:30px;     /* 设置左边内间距30px */ 
padding-right:40px;    /* 设置右边内间距40px */ 
padding-bottom:50px;   /* 设置底部内间距50px */
```

上面的设置可以简写如下：

```
padding：20px 40px 50px 30px; /* 四个值按照顺时针方向，分别设置的是 上 右 下 左  
四个方向的内边距值。 */
```

padding后面还可以跟3个值，2个值和1个值，它们分别设置的项目如下：

```
padding：20px 40px 50px; /* 设置顶部内边距为20px，左右内边距为40px，底部内边距为50px */ 
padding：20px 40px; /* 设置上下内边距为20px，左右内边距为40px*/ 
padding：20px; /* 设置四边内边距为20px */
```

**设置外间距margin**

外边距的设置方法和padding的设置方法相同，将上面设置项中的'padding'换成'margin'就是外边距设置方法。

**盒子模型的尺寸**

按照下面代码制作页面：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>盒子的真实尺寸</title>
    <style type="text/css">
        .box01{width:50px;height:50px;background-color:gold;}
        .box02{width:50px;height:50px;background-color:gold;border:50px
         solid #000}
        .box03{width:50px;height:50px;background-color:gold;border:50px
         solid #000;padding: 50px;}
    </style>
</head>
<body>
    <div class="box01">1</div>
    <br />
    <div class="box02">2</div>
    <br />
    <div class="box03">3</div>
</body>
</html>
```

页面显示效果如下：

![image](https://note.youdao.com/yws/res/2505/42664B90472C4CDC83EC99F54A9FF908)

通过上面的页面得出结论：盒子的width和height设置的是盒子内容的宽和高，不是盒子本身的宽和高，盒子的真实尺寸计算公式如下：

- 盒子宽度 = width + padding左右 + border左右
- 盒子高度 = height + padding上下 + border上下

**思考题：**
1.在布局中，如果我想增大内容和边框的距离，又不想改变盒子显示的尺寸，应该怎么做？

**课堂练习** 
请制作图中所示的标题：

![image](https://note.youdao.com/yws/res/2506/F06003952B624E0DA4C5F0F01C37B946)

**margin相关技巧** 
1、设置元素水平居中： margin:x auto;
2、margin负值让元素位移及边框合并

**外边距合并**

外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。解决方法如下：

1、使用这种特性
2、设置一边的外边距，一般设置margin-top
3、将元素浮动或者定位

**margin-top 塌陷**

在两个盒子嵌套时候，内部的盒子设置的margin-top会加到外边的盒子上，导致内部的盒子margin-top设置失败，解决方法如下：

1、外部盒子设置一个边框
2、外部盒子设置 overflow:hidden
3、使用伪元素类：

```
.clearfix:before{
    content: '';
    display:table;
}
```

### 5.7.圆角边框 ###

5.7.1. border-radis 圆角边框

	取值:
		1. 具体像素
		2. 百分比 50%为圆形

### 5.8 溢出 ###
	ovreflow 处理元素内容溢出部分
	取值:
	1. visible	默认值。内容不会被修剪，会呈现在元素框之外。
	2. hidden	内容会被修剪，并且其余内容是不可见的。
	3. scroll	内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。
	4. auto	如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。


### 5.9.盒子阴影 ###

	box-shadow

### 5.10.元素显示和隐藏 ###

	display:none 
	
	visibility:hidden
	
	区别：
	1. visibility:hidden可以隐藏某个元素，但隐藏的元素仍需占用与未隐藏之前一样的空间
	2. display:none可以隐藏某个元素，且隐藏的元素不会占用任何空间。

### 5.11. float 浮动 ###
	标准文档流 
	文档流，是指盒子按照html标签编写的顺序依次从上到下，从左到右排列，块元素占一行，行内元素在一行之内从左到右排列，先写的先排列，后写的排在后面，每个盒子都占据自己的位置。
	
	浮动特性
	
	1、浮动元素有左浮动(float:left)和右浮动(float:right)两种
	
	2、浮动的元素会向左或向右浮动，碰到父元素边界、浮动元素、未浮动的元素才停下来
	
	3、相邻浮动的块元素可以并在一行，超出父级宽度就换行
	
	4、浮动让行内元素或块元素自动转化为行内块元素
	
	5、浮动元素后面没有浮动的元素会占据浮动元素的位置，没有浮动的元素内的文字会避开浮动的元素，形成文字饶图的效果
	
	6、父元素内整体浮动的元素无法撑开父元素，需要清除浮动
	
	7、浮动元素之间没有垂直margin的合并
	
	清除浮动
	
	父级上增加属性overflow：hidden
	在最后一个子元素的后面加一个空的div，给它样式属性 clear:both（不推荐）
	使用成熟的清浮动样式类，clearfix
	.clearfix:after,.clearfix:before{ content: "";display: table;}
	.clearfix:after{ clear:both;}
	.clearfix{zoom:1;}
	清除浮动的使用方法：
	.con2{... overflow:hidden}
	或者
	<div class="con2 clearfix">
### 5.12.position 定位 ###
我们可以使用css的position属性来设置元素的定位类型，postion的设置项如下：

- relative 生成相对定位元素，元素所占据的文档流的位置不变，元素本身相对文档流的位置进行偏移
- absolute 生成绝对定位元素，元素脱离文档流，不占据文档流的位置，可以理解为漂浮在文档流的上方，相对于上一个设置了相对或者绝对或者固定定位的父级元素来进行定位，如果找不到，则相对于body元素进行定位。
- fixed 生成固定定位元素，元素脱离文档流，不占据文档流的位置，可以理解为漂浮在文档流的上方，相对于浏览器窗口进行定位。
- static 默认值，没有定位，元素出现在正常的文档流中，相当于取消定位属性或者不设置定位属性
- inherit 从父元素继承 position 属性的值

**定位元素特性** 
绝对定位和固定定位的块元素和行内元素会自动转化为行内块元素

**定位元素层级** 
定位元素是浮动的正常的文档流之上的，可以用z-index属性来设置元素的层级

**典型定位布局** 
1、固定在顶部的菜单
2、水平垂直居中的弹框
3、固定的侧边的工具栏
4、固定在底部的按钮

## 6.CSS权重

CSS权重指的是样式的优先级，有两条或多条样式作用于一个元素，权重高的那条样式对元素起作用,权重相同的，后写的样式会覆盖前面写的样式。

### 6.1.权重的等级

可以把样式的应用方式分为几个等级，按照等级来计算权重

1、!important，加在样式属性值后，权重值为 10000
2、内联样式，如：style=””，权重值为1000
3、ID选择器，如：#content，权重值为100
4、类，伪类和属性选择器，如： content、:hover 权重值为10
5、标签选择器和伪元素选择器，如：div、p、:before 权重值为1
6、通用选择器（*）、子选择器（>）、相邻选择器（+）、同胞选择器（~）、权重值为0

### 6.2.权重的计算实例

1、实例一：

```
<style type="text/css">
    div{
        color:red !important;
    }        
</style>
......
<div style="color:blue">这是一个div元素</div>
<!-- 
两条样式同时作用一个div，上面的样式权重值为10000+1，下面的行间样式的权重值为1000，
所以文字的最终颜色为red 
-->
```

2、实例二：

```
<style type="text/css">
    #content div.main_content h2{
        color:red;    
    }
    #content .main_content h2{
        color:blue;
    }
</style>
......
<div id="content">
    <div class="main_content">
        <h2>这是一个h2标题</h2>
    </div>
</div>
<!-- 
第一条样式的权重计算： 100+1+10+1，结果为112；
第二条样式的权重计算： 100+10+1，结果为111；
h2标题的最终颜色为red
-->
```

## 7.CSS3 transform变形

1、translate(x,y) 设置盒子位移
2、scale(x,y) 设置盒子缩放
3、rotate(deg) 设置盒子旋转
4、skew(x-angle,y-angle) 设置盒子斜切
5、perspective 设置透视距离
6、transform-style flat | preserve-3d 设置盒子是否按3d空间显示
7、translateX、translateY、translateZ 设置三维移动
8、rotateX、rotateY、rotateZ 设置三维旋转
9、scaleX、scaleY、scaleZ 设置三维缩放
10、tranform-origin 设置变形的中心点
11、backface-visibility 设置盒子背面是否可见

**举例：（翻面效果）**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>翻面</title>
    <style type="text/css">
        .box{
            width:300px;
            height:272px;
            margin:50px auto 0;
            transform-style:preserve-3d;
            position:relative;            
        }
        .box .pic{
            width:300px;
            height:272px;
            position:absolute;
            background-color:cyan;
            left:0;
            top:0;
            transform:perspective(800px) rotateY(0deg);
            backface-visibility:hidden;
            transition:all 500ms ease;
        }
        .box .back_info{
            width:300px;
            height:272px;
            text-align:center;
            line-height:272px;
            background-color:gold;
            position:absolute;
            left:0;
            top:0;
            transform:rotateY(180deg);
            backface-visibility:hidden;
            transition:all 500ms ease;            
        }
        .box:hover .pic{
            transform:perspective(800px) rotateY(180deg);
        }
        .box:hover .back_info{
            transform:perspective(800px) rotateY(0deg);
        }
    </style>
</head>
<body>
    <div class="box">        
        <div class="pic"><img src="images/location_bg.jpg"></div>
        <div class="back_info">背面文字说明</div>
    </div>
</body>
</html>
```

## 8.CSS3 transition过渡

1、transition-property 设置过渡的属性，比如：width height background-color
2、transition-duration 设置过渡的时间，比如：1s 500ms
3、transition-timing-function 设置过渡的运动方式

- linear 匀速
- ease 开始和结束慢速
- ease-in 开始是慢速
- ease-out 结束时慢速
- ease-in-out 开始和结束时慢速
- cubic-bezier(n,n,n,n)
  - 比如：cubic-bezier(0.845, -0.375, 0.215, 1.335)
  - 曲线设置网站：<https://matthewlein.com/ceaser/>

4、transition-delay 设置动画的延迟
5、transition: property duration timing-function delay 同时设置四个属性

**举例：**

```
<style type="text/css">        
.box{
    width:100px;
    height:100px;
    background-color:gold;
    transition:width 300ms ease,height 300ms ease 300ms,background-color 300ms ease 600ms;            
}
.box:hover{
    width:300px;
    height:300px;
    background-color:red;
}
</style>
......
<div class="box"></div>
```

## 9.CSS3 animation动画

1、@keyframes 定义关键帧动画
2、animation-name 动画名称
3、animation-duration 动画时间
4、animation-timing-function 动画曲线

- linear 匀速
- ease 开始和结束慢速
- ease-in 开始是慢速
- ease-out 结束时慢速
- ease-in-out 开始和结束时慢速
- steps 动画步数

5、animation-delay 动画延迟
6、animation-iteration-count 动画播放次数 n|infinite
7、animation-direction

- normal 默认动画结束不返回
- Alternate 动画结束后返回

8、animation-play-state 动画状态

- paused 停止
- running 运动

9、animation-fill-mode 动画前后的状态

- none 不改变默认行为
- forwards 当动画完成后，保持最后一个属性值（在最后一个关键帧中定义）
- backwards 在 animation-delay 所指定的一段时间内，在动画显示之前，应用开始属性值（在第一个关键帧中定义）
- both 向前和向后填充模式都被应用

10、animation:name duration timing-function delay iteration-count direction;同时设置多个属性

**举例：（人物走路动画）**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>走路动画</title>
    <style type="text/css">        
        .box{
            width:120px;
            height:180px;
            border:1px solid #ccc;            
            margin:50px auto 0;
            position:relative;
            overflow:hidden;            
        }

        .box img{
            display:block;
            width:960px;
            height:182px;
            position: absolute;
            left:0;
            top:0;
            animation:walking 1.0s steps(8) infinite;            
        }
        @keyframes walking{
            from{
                left:0px;
            }

            to{
                left:-960px;
            }
        }
    </style>
</head>
<body>
    <div class="box"><img src="images/walking.png"></div>
</body>
</html>
```

动画中使用的图片如下：

![image](https://note.youdao.com/yws/res/2507/5285903118864C7296AE79ABEE7049FE)
## 7.浏览器兼容配置 ##

为了让CSS3样式兼容，需要将某些样式加上浏览器前缀：

-ms- 兼容IE浏览器
-moz- 兼容firefox
-o- 兼容opera
-webkit- 兼容chrome 和 safari

比如：

```
div
{    
    -ms-transform: rotate(30deg);        
    -webkit-transform: rotate(30deg);    
    -o-transform: rotate(30deg);        
    -moz-transform: rotate(30deg);    
    transform: rotate(30deg);
}
```

**自动添加浏览器前缀**

目前的状况是，有些CSS3属性需要加前缀，有些不需要加，有些只需要加一部分，这些加前缀的工作可以交给插件来完成，比如安装： autoprefixer
