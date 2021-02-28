### 查询DOM信息

    * 访问HTML属性（id、class、style、自定义属性）————> .attr('class')
    * 查看HTML/文本信息 ————> .html()/text()
    * 查看表单值信息 ————> .val()
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>查询DOM</title>
	<link rel="stylesheet" href="">
	<!-- 引入jquery-3.4.1.js库 -->
	<script src='jquery/jquery-3.4.1.js' type='text/javascript'></script>
</head>
<body>	
	<input type="text" name="username" id="username" class="input-text user-input" my-user='张三'>
	<input type="password" name="password">

	<p class="area city">北京</p>
	<p style="color:#f00;">上海</p>
	<p class="area" id="guangzhou">广州</p>
	<p>深圳</p>

	<script>
		$(function() {
			// class属性
			var cls = $('#username').attr('class');
			console.log(cls);
			// type属性
			var tps = $('#username').attr('type');
			console.log(tps);
			// 自定义属性
			var my = $('#username').attr('my-user');
			console.log(my);
		});
	</script>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>查询DOM</title>
	<link rel="stylesheet" href="">
	<!-- 引入jquery-3.4.1.js库 -->
	<script src='jquery/jquery-3.4.1.js' type='text/javascript'></script>
</head>
<body>	
	<input type="text" name="username" id="username" class="input-text user-input" my-user='张三' value="我的用户名">
	<!-- textarea select checkbox radio -->
	<input type="password" name="password">

	<p class="area city">北京</p>
	<p style="color:#f00;">上海</p>
	<p class="area" id="guangzhou">广州</p>
	<p>深圳</p>
	
	<p class="info" id="info">
		<span>内容：</span>
		<small>文字描述</small>
	</p>
	<script>
		$(function() {
			// 查询html信息
			var p_html = $('#info').html();
			console.log(p_html);

			// 查询text信息
			var text_info = $('#info').text();
			console.log(text_info);

			// 查询表单值
			var input_username = $('#username').val();
			console.log(input_username);
		});
	</script>
</body>
</html>
```

### jQuery对象与原生DOM对象相互转换

    * $('#id').get(0)  使用get方式转换成DOM对象
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>查询DOM</title>
	<link rel="stylesheet" href="">
	<!-- 引入jquery-3.4.1.js库 -->
	<script src='jquery/jquery-3.4.1.js' type='text/javascript'></script>
</head>
<body>	
	<input type="text" name="username" id="username" class="input-text user-input" my-user='张三' value="我的用户名">
	<!-- textarea select checkbox radio -->
	<input type="password" name="password">

	<p class="area city">北京</p>
	<p style="color:#f00;">上海</p>
	<p class="area" id="guangzhou">广州</p>
	<p>深圳</p>
	
	<p class="info" id="info">
		<span>内容：</span>
		<small>文字描述</small>
	</p>
	<script>
		$(function() {
			// jQuery转换成DOM对象
			var username = $('#username');
			console.log('username jquery', username);
			// dom对象 获取到上面定义的value值
			console.log('username dom', username.get()[0].value);
		});
	</script>
</body>
</html>
```

### jQuery的遍历
    
    * length 对象的长度
    * for循环遍历
    * .each()循环遍历
    * .find()/.children()等筛选操作
        find作用：在当前的元素集合中进行搜索
        语法规则：.find(selector)，直接放入选择器（比如标签、class选择）、或者直接传入元素.find(element)
        
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>查询DOM</title>
	<link rel="stylesheet" href="">
	<!-- 引入jquery-3.4.1.js库 -->
	<script src='jquery/jquery-3.4.1.js' type='text/javascript'></script>
</head>
<body>	
	<input type="text" name="username" id="username" class="input-text user-input" my-user='张三' value="我的用户名">
	<!-- textarea select checkbox radio -->
	<input type="password" name="password">

	<p class="area city">北京</p>
	<p style="color:#f00;">上海</p>
	<p class="area" id="guangzhou">广州</p>
	<p>东莞<span>测试</span></p>
	<p>深圳</p>
	
	<p class="info" id="info">
		<span>内容：</span>
		<small>文字描述</small>
	</p>
	<script>
		$(function() {
			var p_list = $('p');
			console.log(p_list);
			console.log('总共有几个:', p_list.length);

			// for循环遍历
			for (var i=0; i<p_list.length; i++) {
				var item = p_list[i];
				console.log(item);
			}

			// .each()遍历
			console.log('---获取到下标和值---')
			p_list.each(function(index, value) {
				console.log(index, value)
			});

			// 方法二这种方式使用更广泛：json对象数组[{username:}, {},]
			$.each(['aa', 'bb', 'cc'], function(index, value) {
				console.log(index, value);
			});

			// .find的使用
			var list = p_list.find('span');
			console.log(list);
		});
	</script>
</body>
</html>
```
    