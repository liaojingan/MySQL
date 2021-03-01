### jQuery常用事件

    * 文档加载（DOM加载就绪）
    * 鼠标事件（点击、滑动）
    * 键盘事件
    * 表单事件
    
### 文档加载

    * 当DOM准备就绪时，指定一个函数来执行
    * 两种书写方式
        $(document).ready(function() {})
        $(function(){})
        
### 鼠标事件

    * 点击事件  
        .click()/.dblclick() 单击/双击
        .mousedown()/.mouseup() 按下/抬起
        
    * 移动事件
        .mouseenter()/.mouseleave() 进入/离开(快捷写法：hover)
        
### 表单事件
    
    * 焦点事件
        .focus()/.blur() 获得/失去焦点
    
    * 值发生改变事件
        .change()
        
    * form表单的提交
        .submit()
        
### jQuery事件绑定
    
    * 绑定语法方法
        on('click', function(){})
        click(function(){})
        bind('click', function(){})
        
    * 这三者主要是使用上的区别，常用的前两种：
        从服务器上获取html片段，对片段中的某些标签进行绑定，建议使用on事件绑定，bind主要是有了这个元素后进行绑定不推荐使用
        第二种方式简洁
        
        
    js逻辑和html分离
    
```js
<!--文件名my_js.js-->
$(function() {
	// 先查询标签(事件源)再绑定事件
	$('div').click(function() {
		alert('点击');
	});
});


$(function() {
	// 双击事件
	$('div').dblclick(function() {
		alert('双击');
	})
});

$(function() {
	// 双击事件
	$('div').on('click', function() {
		alert('同样的方式');
	})
});
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
	<div>点击</div>
	<!-- 引入js -->
	<script src="./my_js.js">
		
	</script>
</body>
</html>
```

    * 鼠标移入和移出事件绑定(html文档同上)
    
```js
$(function() {
	// 双击事件
	$('div').mouseenter(function() {
		$(this).css({
			'background-color': '#f00'
		})
		// 链式调用
	}).mouseleave(function() {
		$(this).css({
			'background-color': '#fff'
		})
	})
});
```

    * 用hover代替mouseenter和mouseleave
    
```js
$(function() {
	$('div').hover(function() {
		$(this).css({
			'background-color': '#00f'
		})
	}, function() {
		$(this).css({
			'background-color': '#fff'
		})
	})
});
```

    * 键盘事件  
        按下按键抬起时，打印内容
        
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
	<div>点击</div>
	<input type="text" name="username" id="username">
	<!-- 引入js -->
	<script src="./my_js.js">
		
	</script>
</body>
</html>
```

```js
$(function() {
	// 键盘事件
	$('#username').keyup(function() {
		// 获取值
		var val = $(this).val();
		console.log(val);
	})
});
```

    * 表单事件：打开网页输入框就获取到了焦点，点击其他位置就失去焦点

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<title>jQuery事件</title>
	<script src="./js/jquery-3.4.1.js" type="text/javascript"></script>
	<style type="text/css">
		.text-danger {
			color: #f00;
		}
		.reg3 {
			background-color: #f00;
			padding: 30px;
		}
		.reg3 span {
			background-color: #fff;
		}
	</style>
</head>
<body>
	<!-- <div onclick="clickMe()">请点击我</div> -->
	<div >请点击我</div>
	<input type="text" name="username" id="username">
	<form action="." method="get">
		<input type="text" name="uname" id="uname">
		<p id="txtError" class="text-danger"></p>
		<select name="sex" id="sex">
			<option value="1">男</option>
			<option value="0">女</option>
		</select>
		<input type="password" name="password">
		<input type="submit" value="注册">
		<button type="submit">提交</button>
	</form>
	<a class="reg2" href="http://imooc.com">注册</a>
	<a class="reg" href="javascript:;">注册会员</a>
	<a class="reg" href="javascript:void(0);">注册会员</a>

	<a class="reg3" href="avascript:;">
		<span>点击我</span>
	</a>
	<script type="text/javascript" src="js/jquery-3.4.1.js">
		// function clickMe() {
		// 	alert('点击了我')
		// }
		// $(function() {
		// 	// js业务逻辑和html分离
		// 	$('div').click(function() {
		// 		alert('点击了')
		// 	})
		// })
	</script>
</body>
</html>
```

```js
$(function() {
	// 用户名获取焦点
	$("#uname").foucs();

	$("#uname").blur(function() {
		var phone = $(this).val()
		// 输入数值不等于11位就将错误信息显示在P标签中
		if (phone.length !== 11) {
			$('#txtError').text('输入的手机号码不正确~')
		} 
	})
});
```

    * 性别选择发生变化触发.change()值改变事件
 
```js
$(function() {
	// 性别选择发生变化时触发
	$('#sex').change(function() {
		var sex = $(this).val();
		console.log(sex); 
	})

});
```

    * 表单验证
      type="submit" 为表单触发事件
      return false  可阻止表单提交
      
```js
$(function() {
	// 性别选择发生变化时触发
	$('#sex').change(function() {
		var sex = $(this).val();
		console.log(sex); 
	})

	$('form').submit(function() {
		alert('表单提交了~');
		// 验证表单内容，比如用户名、密码等
		// 验证通过了，才提交表单，验证失败返回false
		return false;  // 阻止了表单的提交
	})
});
```

### 事件的行为

    * 阻止a标签的默认行为
    
    方法一
    
```js
$(function() {
	// a标签的事件
	$('a').click(function(event) {
		// 弹出弹窗点击确认后默认行为是跳转到慕课网
		// 要阻止a标签的默认行为，需传入event参数，使用event.preventDefault()
		event.preventDefault();
		alert('a click');
	});
});
```

    方法二：先在html文件添加，指定href特定的字符串
    // <a class="reg" href="javascript:;">注册会员</a>
	// <a class="reg" href="javascript:void(0);">注册会员</a>
	
```js
$(function() {
	// a标签的事件
	$('.reg2').click(function(event) {
		alert('a click 2');
	});
});
```

    * 阻止多个事件冒泡行为
        event.stopPropagation()
        
      元素嵌套时，点击里面的元素因为事件的冒泡也会触发外面的事件
      希望点击span标签时，不触发外面a标签事件，所以在span标签上阻止冒泡
      
```js
$(function() {
	// 事件的冒泡
	$('.reg3').click(function() {
		alert('reg3');
	});

	$('.reg3 span').click(function(e) {
		// 阻止事件冒泡
		e.stopPropagation();
		alert('reg3 span');
	});
});
```

### 使用jQuery做什么

    * 查询/操作DOM
    * 处理JS事件
    * 实现动画效果
    * 封装使用jQuery插件
    * 使用Ajax发送异步请求
        
        
	
	
    
    
    
 