# web前端-chapt05 #

## 1.jQuery简介 ##
jQuery是目前使用最广泛的javascript函数库。据统计，全世界排名前100万的网站，有46%使用jQuery，远远超过其他库。微软公司甚至把jQuery作为他们的官方库。

jQuery的版本分为1.x系列和2.x、3.x系列，1.x系列兼容低版本的浏览器，2.x、3.x系列放弃支持低版本浏览器，目前使用最多的是1.x系列的。

jquery是一个函数库，一个js文件，页面用script标签引入这个js文件就可以使用。

```
<script type="text/javascript" src="js/jquery-1.12.2.js"></script>
```

jquery的口号和愿望 Write Less, Do More（写得少，做得多）

1、<http://jquery.com/> 官方网站
2、<https://code.jquery.com/> 版本下载

## 2.jQuery下载和引入 ##

jQuery 官网:

	https://jquery.com/

下载压缩过的版本(体积小,用于产品,代码不可读):

Download the compressed, production jQuery 3.4.1

下载未压缩过的版本(体积大,用于生产,代码可读):

Download the uncompressed, development jQuery 3.4.1

## 3.使用CDN引入jQuery ##

如果不希望下载并存放 jQuery，那么也可以通过 CDN（内容分发网络） 引用它。

Staticfile CDN、百度、又拍云、新浪、谷歌和微软的服务器都存有 jQuery 。

如果站点用户是国内的，建议使用百度、又拍云、新浪等国内CDN地址，如果站点用户是国外的可以使用谷歌和微软。

百度 CDN:

	<script src="https://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script>

新浪 CDN:

	<script src="https://lib.sinaapp.com/js/jquery/2.0.2/jquery-2.0.2.min.js"></script>

Google CDN:

	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>

Microsoft CDN:

	<script src="https://ajax.aspnetcdn.com/ajax/jquery/jquery-1.9.0.min.js"></script>

## 4.jQuery 语法 ##

jQuery 语法是通过选取 HTML 元素，并对选取的元素执行某些操作。

基础语法： 

	$(selector).action()
	
	或者
	
	jQuery(selector).action()
	
	1. $ 可以看作是 jQuery对象的别名
	2. selector 可以是:
		1. css选择器
		2. 一段html代码
		3. this 关键字
		4. js 对象
	3. action () 是jQuery函数

## 5.jquery加载

将获取元素的语句写到页面头部，会因为元素还没有加载而出错，jquery提供了ready方法解决这个问题，它的速度比原生的 window.onload 更快。

```
<script type="text/javascript">

$(document).ready(function(){

     ......

});

</script>
```

可以简写为：

```
<script type="text/javascript">

$(function(){

     ......

});

</script>
```

## 6.jquery选择器

**jquery用法思想**一 
选择某个网页元素，然后对它进行某种操作

**jquery选择器** 
jquery选择器可以快速地选择元素，选择规则和css样式相同，使用length属性判断是否选择成功。

```
$(document) //选择整个文档对象
$('li') //选择所有的li元素
$('#myId') //选择id为myId的网页元素
$('.myClass') // 选择class为myClass的元素
$('input[name=first]') // 选择name属性等于first的input元素
$('#ul1 li span') //选择id为为ul1元素下的所有li下的span元素
```

**对选择集进行修饰过滤(类似CSS伪类)**

```
$('#ul1 li:first') //选择id为ul1元素下的第一个li
$('#ul1 li:odd') //选择id为ul1元素下的li的奇数行
$('#ul1 li:eq(2)') //选择id为ul1元素下的第3个li
$('#ul1 li:gt(2)') // 选择id为ul1元素下的前三个之后的li
$('#myForm :input') // 选择表单中的input元素
$('div:visible') //选择可见的div元素
```

**对选择集进行函数过滤**

```
$('div').has('p'); // 选择包含p元素的div元素
$('div').not('.myClass'); //选择class不等于myClass的div元素
$('div').filter('.myClass'); //选择class等于myClass的div元素
$('div').first(); //选择第1个div元素
$('div').eq(5); //选择第6个div元素
```

**选择集转移**

```
$('div').prev('p'); //选择div元素前面的第一个p元素
$('div').next('p'); //选择div元素后面的第一个p元素
$('div').closest('form'); //选择离div最近的那个form父元素
$('div').parent(); //选择div的父元素
$('div').children(); //选择div的所有子元素
$('div').siblings(); //选择div的同级元素
$('div').find('.myClass'); //选择div内的class等于myClass的元素
```

## 7.jquery样式操作

**jquery用法思想**二
同一个函数完成取值和赋值

**操作行间样式**

```
// 获取div的样式
$("div").css("width");
$("div").css("color");


//设置div的样式
$("div").css("width","30px");
$("div").css("height","30px");
$("div").css({fontSize:"30px",color:"red"});
```

**特别注意** 
选择器获取的多个元素，获取信息获取的是第一个，比如：$("div").css("width")，获取的是第一个div的width。

**操作样式类名**

```
$("#div1").addClass("divClass2") //为id为div1的对象追加样式divClass2
$("#div1").removeClass("divClass")  //移除id为div1的对象的class名为divClass的样式
$("#div1").removeClass("divClass divClass2") //移除多个样式
$("#div1").toggleClass("anotherClass") //重复切换anotherClass样式
```

## 8.jquery属性操作

1、html() 取出或设置html内容

```
// 取出html内容

var $htm = $('#div1').html();

// 设置html内容

$('#div1').html('<span>添加文字</span>');
```

2、text() 取出或设置text内容

```
// 取出文本内容

var $htm = $('#div1').text();

// 设置文本内容

$('#div1').text('<span>添加文字</span>');
```

3、attr() 取出或设置某个属性的值

```
// 取出图片的地址

var $src = $('#img1').attr('src');

// 设置图片的地址和alt属性

$('#img1').attr({ src: "test.jpg", alt: "Test Image" });
```

## 9.绑定click事件

给元素绑定click事件，可以用如下方法：

```
$('#btn1').click(function(){

    // 内部的this指的是原生对象

    // 使用jquery对象用 $(this)

})
```

## 10.jquery特殊效果

```
fadeIn() 淡入

    $btn.click(function(){

        $('#div1').fadeIn(1000,'swing',function(){
            alert('done!');
        });

    });

fadeOut() 淡出
fadeToggle() 切换淡入淡出
hide() 隐藏元素
show() 显示元素
toggle() 依次展示或隐藏某个元素
slideDown() 向下展开
slideUp() 向上卷起
slideToggle() 依次展开或卷起某个元素
```





## 14.jquery事件

**事件函数列表：**

```
blur() 元素失去焦点
focus() 元素获得焦点
change() 表单元素的值发生变化
click() 鼠标单击
dblclick() 鼠标双击
mouseover() 鼠标进入（进入子元素也触发）
mouseout() 鼠标离开（离开子元素也触发）
mouseenter() 鼠标进入（进入子元素不触发）
mouseleave() 鼠标离开（离开子元素不触发）
hover() 同时为mouseenter和mouseleave事件指定处理函数
mouseup() 松开鼠标
mousedown() 按下鼠标
mousemove() 鼠标在元素内部移动
keydown() 按下键盘
keypress() 按下键盘
keyup() 松开键盘
load() 元素加载完毕
ready() DOM加载完成
resize() 浏览器窗口的大小发生改变
scroll() 滚动条的位置发生变化
select() 用户选中文本框中的内容
submit() 用户递交表单
toggle() 根据鼠标点击的次数，依次运行多个函数
unload() 用户离开页面
```






