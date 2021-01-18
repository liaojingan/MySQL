    css :层叠样式表 (Cascading Style Sheets)（级联样式表）
>**基础选择器**1、标签选择器（总结：一打一大片）
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	<title>Document</title>
	<style type="text/css">
		div{
			color: blue;
			font-size: 16px;
		}
		p{
			color: brown;
			font-size: 20px;
		}
	</style>
</head>
<body>
	<div>也许遗憾总是和年轻绑在一起</div>
	<p>我若不勇敢，谁来替我坚强</p>
</body>
</html>
```
    用途：批量处理或清空默认样式。
    
>2、id选择器（总结：只能打一个）
>>写法： #自定义名称{属性:值;}
```html
<style type="text/css">
/*ID选择器*/
#box{
   font-size: 12px;
   color: red;
   backgroud-color: rgb(250,234,12);
}
</style>
</head>
<body>
    <div id="box">戴上面具我就失去了自己，可是摘下面具我便失去了世界。</div>
</body>
```
    每个标签都有id属性，id属性值由字母开头，后面可以为数字、下划线、横线;
    id属性值需要区分大小写；
    id在页面中保持唯一性；
    
>缺点：对多个元素设置同样的样式的时候，需要起多个id,写多次重复的样式，会造成代码冗余
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	<title>Document</title>
	<style type="text/css">
	/*如果id="p1"和id="p2"都有字体大小、颜色相同的样式，则要书写两次，就会出现代码冗余*/
	#p1 {
		font-size: 16px;
		color: red;
	}
	#p2 {
		font-size: 16px;
		color: red;
	}
		
	</style>
</head>
<body>
	<p id="p1">CSS是层叠样式表</p>
	<div>
		<div>
			<p id="p2">珍惜黄昏的村庄，珍惜雨水的村庄，万里无云，如同我永恒的悲伤。</p>
		</div>
	</div>
</body>
</html>
```   
>3、(重点：class类选择器)类选择器 （总结：谁调用谁生效，指谁打谁）
    
    1、class属性值不是唯一的；允许重复（不同标签可以取相同的class名）

    2、作用：可以用类选择器去选择一部分相同的样式;

    3、一个标签的class值是可以有多个的，用空格分开;

    4、与id选择器区别
        id属性一般用于js；   类用于设置样式；
        总结：类上样式，id上行为
    工作中：一般使用class类时，先把公共的类抽取出来，分解成“原子类"。示例如下    
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	<title>Document</title>
	<style type="text/css">
		/*需求：第一个p元素设置下划线、颜色为红色；
		第二个p元素设置下划线、字号为24px；
		第三个p元素设置颜色为红色，字号为24px;*/

		/*样式涉及颜色、下划线、字号
		三个p元素样式只不过是前面的样式的组合*/
		.red {
			color: red;
		}
		.xiahuaxian {
			text-decoration: underline;
		}
		.f18 {
			font-size: 18px;
		}
	</style>
</head>
<body>
	<p class="xiahuaxian red">未了，重生，时间能否会让这一切重来，慢慢等着，等着。</p>
	<p class="xiahuaxian f18">车窗外的云彩暗了，时已薄暮，淅淅沥沥，好像下起雨来了。</p>
	<p class="red f18">你是谁朝思暮想的笔尖少年，在绝望的荒途里辗转成歌。</p>
</body>
</html>
```
        
>4、通配符选择器(*)了解即可
    
    效率比较低，在实际项目中不再使用
    
    可使用的地方：清除默认样式：下方实例的第二种方式的写法效率相对较高
```html
<!--清除默认样式方式一-->
*{
　　padding: 0;
　　margin: 0;
}

<!--方式二-->
blockquote,body,button,ul{margin:0;padding:0}
```

>高级选择器 5、后代选择器
>> 写法： 选择器+空格+选择器+空格+......+选择器{属性:值;}
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	<title>Document</title>
	<style type="text/css">
		/*通过层级的结构(后代选择器)定位元素：选中“Jmeter和性能测试”*/
		div ul li {
			text-decoration: underline;
			color: red;
		}
		/*中间可以无限次隔代：选中“HTML超文本标记语言和CSS层叠样式表”*/
		div p {
			font-size: 18px;
			background-color: green;
		}
		/*可以类选择器和标签选择器等相互结合定位元素：选中“Selenium webdriver”*/
		ul .box {
			color: green;
		}
	</style>
</head>
<body>
	<ol>
		<li>Python语言</li>
		<li>Java语言</li>
	</ol>
	<ul>
		<li class="box">Selenium webdriver</li>
		<li>自动化测试</li>
	</ul>
	<div>
		<ul>
			<li>Jmeter</li>
			<li>性能测试</li>
		</ul>
	</div>
	<div>
		<div>
			<div>
				<p>HTML超文本标记语言</p>
			</div>
		</div>
	</div>
	<div>
		<div>
			<p>CSS层叠样式表</p>
		</div>
	</div>
</body>
</html>
```

>6、交集选择器 
>>写法：标签+类（ID）选择器{属性:值;}   注意：中间没有空格

    特点：既要满足使用了某种标签，同时还要满足使用了类（ID）选择器；
    .demo.demo2 -->以上写法一般都可以, 但在ie6不支持类名连续交集。
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	<title>Document</title>
	<style type="text/css">
		/*交集选择器就可只定位到第一个p元素*/
		p.demo {
			font-size: 22px;
			font-weight: 700;
		}
		/*此种写法存在兼容性问题*/
		.demo.box {
			color: green;
		}
	</style>
</head>
<body>
	<p class="demo">
		你走吧，我总要习惯一个人。
	</p>
	<p>
		戴上面具我就失去了自己，可是摘下面具我便失去了世界。
	</p>
	<div class="demo" id="box">
		你是谁朝思暮想的笔尖少年，在绝望的荒途里辗转成歌。
	</div>
</body>
</html>
```
    
>7、并集选择器 写法：选择器+，+选择器+,+...+选择器{属性:值;}

    选中多个标签，用逗号分隔开。
    
    应用场景：多个标签样式相同，一个选择器选不完；
            设置页面整体的默认样式。
            blockquote,body,button,ul,dd,dt,input,li,th,textarea{margin:0;padding:0}
