### jQuery与JS关系

    jQuery是一个高效、精简并且功能丰富的JavaScript工具库
    jQuery核心思想：write less, do more
    
### jQuery特点
    
    * 易于使用的API接口（支持链式调用）
    * 能够兼容众多浏览器
    * 使用非常的广泛
    
### 使用jQuery做什么

    * 查询/操作DOM
    * 处理JS事件
    * 实现一些动画效果
    * 封装/使用jQuery插件
    * 使用Ajax发送异步请求
    （浏览器F12审查元素——XHR中可以查看到请求，用户可以第一事件看到结构，优先级不高的可以使用异步请求实现）
    
### 版本选择
    
    需要下载
    * 源码版本（用于开发环境）jquery.js
    * 压缩版（用于生产环境）jquery.min.js
    
### jQuery操作DOM

    目标： 理解jQuery对象和DOM对象；选择器；遍历DOM及属性、修改DOM；链式调用
    
    使用原生JS实现查询
        * 根据ID查询 getElementById
        * 根据class查询 getElementsByClassName
        * 根据标签查询 getElementsByTagName
        
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>	
	<input type="text" name="username" id="username">
	<p class="area">北京</p>
	<p class="area">上海</p>
	<p class="area">广州</p>
	<p>深圳</p>
	<script>
		var Oid = document.getElementById("username");
		console.log(Oid);

		var area_list = document.getElementsByClassName("area");
		console.log(area_list);

		var p_list = document.getElementsByTagName("p");
		console.log(p_list);
	</script>
</body>
</html>
```
 
    使用上面原生的方法进行查询的代码量较多
    
    1、 实现jQuery的id选择器
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>	
	<input type="text" name="username" id="username">
	<p class="area">北京</p>
	<p class="area">上海</p>
	<p class="area" id="guangzhou">广州</p>
	<p>深圳</p>
	<script>
		// jQuery实现id选择器
		var $ = function(id) {
			return document.getElementById(id);
		};

		console.log($("username"));
		console.log($("guangzhou"));
	</script>
</body>
</html>
```

### jQuery选择器

    * #id选择器
    * element(元素)选择器
    * .class选择器
    * 层级选择（父子、兄弟等）
    * 伪类选择器
    * 属性选择器
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>jQuery选择器使用</title>
	<link rel="stylesheet" href="">
	<!-- 引入jquery-3.4.1.js库 -->
	<script src='jquery/jquery-3.4.1.js' type='text/javascript'></script>
	<script>
		// jQuery查找代码放在行内只是打印出对象，还没转换成DOM树，所以需要代码放到下面代码中
		// $(document).ready(function()表示我的文档已经解析完成了，DOM树生成了，jQuery下载好了
		$(document).ready(function() {
			// jQuery代码内容
			// 根据id $函数就是jQuery提供的
			var username = $("#username");
			console.log(username);

			// 根据class查询
			var area_list = jQuery('.area');
			console.log(area_list);

			// 根据元素的标签查询
			var p_list = $("p");
			console.log(p_list);	
		})  
		
	</script>
</head>
<body>	
	<input type="text" name="username" id="username">
	<p class="area">北京</p>
	<p class="area">上海</p>
	<p class="area" id="guangzhou">广州</p>
	<p>深圳</p>
</body>
</html>
```

    上面的$(document).ready(function()可以简写成$(function()
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>jQuery选择器使用</title>
	<link rel="stylesheet" href="">
	<!-- 引入jquery-3.4.1.js库 -->
	<script src='jquery/jquery-3.4.1.js' type='text/javascript'></script>
	<script>
		// jQuery查找代码放在行内只是打印出对象，还没转换成DOM树，所以需要代码放到下面代码中
		// $(document).ready(function()表示我的文档已经解析完成了，DOM树生成了，jQuery下载好了
		$(function() {
			// jQuery代码内容
			// 根据id $函数就是jQuery提供的
			var username = $("#username");
			console.log(username);

			// 根据class查询
			var area_list = jQuery('.area');
			console.log(area_list);

			// 根据元素的标签查询
			var p_list = $("p");
			console.log(p_list);	
		})  
		
	</script>
</head>
<body>	
	<input type="text" name="username" id="username">
	<p class="area">北京</p>
	<p class="area">上海</p>
	<p class="area" id="guangzhou">广州</p>
	<p>深圳</p>
</body>
</html>
```

### 层级选择器
    
    * $('parent>child') 表示parent元素中的指定的child直接子元素
    * $('parent child') 表示所有后代元素
    * $('prev + next') 表示紧贴prev之后的元素
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>jQuery选择器使用</title>
	<link rel="stylesheet" href="">
	<!-- 引入jquery-3.4.1.js库 -->
	<script src='jquery/jquery-3.4.1.js' type='text/javascript'></script>
	<script>
		// jQuery查找代码放在行内只是打印出对象，还没转换成DOM树，所以需要代码放到下面代码中
		// $(document).ready(function()表示我的文档已经解析完成了，DOM树生成了，jQuery下载好了
		$(function() {
			// 层级选择器 选择body后的所有元素
			var body_list = $('body *'); 	
			console.log(body_list);

			// 查询所有的后代元素p
			var body_p = $('body p'); 
			console.log(body_p);

			// 直接的子元素
			var body_p1 = $('body > p');
			console.log(body_p1);


			// 紧贴之后的元素
			var input = $('label + input');
			console.log(input)
		});
		
	</script>
</head>
<body>	
	<label for="username">用户名</label>
	<input type="text" name="username" id="username">
	<input type="password" name="password">

	<p class="area">北京</p>
	<p class="area">上海</p>
	<p class="area" id="guangzhou">广州</p>
	<p>深圳</p>

	<div>
		<p>海南</p>
	</div>
</body>
</html>
```

### 伪类选择器

    * :first/last 第一个/最后一个匹配的元素
    * :eq(N) 匹配的索引为N的元素
    * :even/:odd 奇数/偶数个元素
    * :checked 表单中所有勾选的元素
    * :disabled 被禁用的元素
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>jQuery选择器使用</title>
	<link rel="stylesheet" href="">
	<!-- 引入jquery-3.4.1.js库 -->
	<script src='jquery/jquery-3.4.1.js' type='text/javascript'></script>
	<script>
		// jQuery查找代码放在行内只是打印出对象，还没转换成DOM树，所以需要代码放到下面代码中
		// $(document).ready(function()表示我的文档已经解析完成了，DOM树生成了，jQuery下载好了
		$(function() {
			// 伪类选择器 选择第一个p标签
			var p_first = $('p:first');
			console.log(p_first);

			// 匹配索引为1的p标签
			var p2 = $('p:eq(1)');
			console.log(p2)
		});
		
	</script>
</head>
<body>	
	<label for="username">用户名</label>
	<input type="text" name="username" id="username">
	<input type="password" name="password">

	<p class="area">北京</p>
	<p class="area">上海</p>
	<p class="area" id="guangzhou">广州</p>
	<p>深圳</p>

	<div>
		<p>海南</p>
	</div>
</body>
</html>
```

### 属性选择器

    例如：
        * $('input[name='password']) 表示选择input标签且name属性是password
        * $('input[name]) 表示inpu标签只要有name属性就查询
        
    属性选择器常用条件
        * =: 等于/相等
        * ^=: 以**开始
        * $=: 以**结束
        
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>jQuery选择器使用</title>
	<link rel="stylesheet" href="">
	<!-- 引入jquery-3.4.1.js库 -->
	<script src='jquery/jquery-3.4.1.js' type='text/javascript'></script>
	<script>
		// jQuery查找代码放在行内只是打印出对象，还没转换成DOM树，所以需要代码放到下面代码中
		// $(document).ready(function()表示我的文档已经解析完成了，DOM树生成了，jQuery下载好了
		$(function() {
			// 属性选择器
			var password = $('input[name="password"]');
			console.log(password);

			var inputs = $('input[name]');
			console.log(inputs)
		});
		
	</script>
</head>
<body>	
	<label for="username">用户名</label>
	<input type="text" name="username" id="username">
	<input type="password" name="password">

	<p class="area">北京</p>
	<p class="area">上海</p>
	<p class="area" id="guangzhou">广州</p>
	<p>深圳</p>

	<div>
		<p>海南</p>
	</div>
</body>
</html>
```
    