### 修改DOM信息

    * 使用jQuery构建DOM 使用$('<p/>')
    * 使用.append()/.appendTo()添加到DOM
        .append()前提条件是找到元素，添加到该元素后面
        .appendTo()构建好DOM，然后加载上去
    * .html()/.text()/.val()/.attr()设置内容
    * .show()/hide()控制显示和隐藏
    
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
			// 构建dom对象
			var html = $('<p class="test"/>');
			console.log(html);
			// 将构建的标签添加到body中
			// html.appendTo('body');

			// 直接添加
			$('body').append(html);
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
	<p>东莞<span>测试</span></p>
	<p>深圳</p>
	
	<p class="info" id="info" style="display: none">
		<span>内容：</span>
		<small>文字描述</small>
	</p>
	<script>
		$(function() {
			// 构建dom对象
			var html_dom = $('<p class="test"/>');
			console.log(html_dom);

			// 方法一：在dom中添加内容
			// html_dom.html('<span>新添加的</span>');
			// $('body').append(html_dom);


			// 方法二
			$('#guangzhou').html('<span>新添加的</span>');


			// 添加属性=值，area='666'，attr此方法修改属性后会覆盖
			// $('#guangzhou').attr('area', '666');

			// 此方法不会覆盖，只是再次添加一个新的class
			$('#guangzhou').addClass('666');

			// 移除class
			$('#guangzhou').removeClass('area');

			// 操作css样式
			$('#guangzhou').css({
				'color': '#0f0',
				'background-color': '#000'
			});

			// 隐藏元素
			// $('#guangzhou').hide();

			// 显示元素
			$('#guangzhou').show();
		});
	</script>
</body>
</html>
```

### 链式调用

    * 生成html对象并添加到DOM
        例如：$('<p/>').text('你好').appendTo('#id')  就是一直得到jQuery对象然后继续调用
        
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
	
	<p class="info" id="info" style="display: none">
		<span>内容：</span>
		<small>文字描述</small>
	</p>
	<script>
		$(function() {
			// 链式调用
			var my_dom = $('<p/>').text('你好').append('<span>测试<span/>').appendTo('body');
			
		});
	</script>
</body>
</html>
```