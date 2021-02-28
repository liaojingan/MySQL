1、事件绑定

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
	   // window.onload = function() {}
	   // onload事件页面加载完触发该事件
	   onload = function() {
	   	   /*
          事件源.事件 = function() {
          // 事件处理函数
          }

	    */
	    // 找到事件源 ------- 根据id找元素
	    var oBtn = document.getElementById("btn");
        //alert(oBtn); 
        // onclick 单击
        oBtn.onclick = function() {
        	// 事件发生后会执行的操作
        	alert("你好啊");
        }
	   }
	    
	</script>
	<button id="btn">点我一下试试</button>
</body>
</html>
```

2、元素的显示和隐藏

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <button id="btn">显示</button>
    <button id="btn1">隐藏</button>
    <div id="box">div模块</div>
    <script>
        oBtn = document.getElementById("btn");
        oBtn1 = document.getElementById("btn1");
        oBox = document.getElementById("box");

        oBox.style.width = "200px";
        oBox.style.height = "200px";
        oBox.style.background = "pink";

        oBtn.onclick = function() {
            oBox.style.display = "block";
        }

        oBtn1.onclick =function() {
            oBox.style.display = "none";
        }
    </script>
</body>
</html>
```

3、切换图片

```htm
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<img src="jy.jpg" alt="">
	<script type="text/javascript">
	    // 鼠标放入图片元素 显示另外一张图片
	    // 1 找事件源 
	    // 注意：根据标签名找 结果是一个集合 使用时候需要按照数组方式用
		// 以下方法没有兼容，只能在谷歌浏览器实现
	    var oImg = document.getElementsByTagName("img")[0];
	    // 2 绑定事件
	    oImg.onmouseover = function() {
	    	//alert("hello");
	    	oImg.src = "tlbb.jpg";
	    }

	    oImg.onmouseout = function() {
	    	//alert("hello");
	    	oImg.src = "jy.jpg";
	    }
	</script>
</body>
</html>
```

4、高亮显示

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style type="text/css">
	    /*li:hover {
	    	background-color: green;
	    }*/
	</style>
</head>
<body>
	<ul>
		<li>北京</li>
		<li>深圳</li>
		<li>上海</li>
		<li>杭州</li>
		<li>广州</li>
	</ul>
	<script type="text/javascript">
	    // 分别给每个li绑定鼠标放上去事件
	    var lis = document.getElementsByTagName("li");
	    // 循环绑定
	    for(var i=0; i<lis.length; i++) {
	    	// 绑定鼠标放上去
	    	lis[i].onmouseover = function() {
	    		// 让当前的li增加背景色
	    		//lis[i].style.background = "green"; 错误 因为鼠标放上去 函数体代码执行 此时i的值是5
	    		// this代表当前事件源（因为有多个li标签，只要鼠标放在任何一个li上都是一个事件源，所以不能用li[i]，而是使用this代表当前）
	    		this.style.background = "green";
	    	}
	    	// 绑定鼠标离开
	    	lis[i].onmouseout= function() {
	    		// this代表当前事件源
	    		this.style.background = "";
	    	}
	    }
	</script>
</body>
</html>
```

5、隔行变色

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style type="text/css">
	    /*li:hover {
	    	background-color: green;
	    }*/
	</style>
</head>
<body>
	<ul>
		<li>北京</li>
		<li>深圳</li>
		<li>上海</li>
		<li>杭州</li>
		<li>广州</li>
		<li>北京</li>
		<li>深圳</li>
		<li>上海</li>
		<li>杭州</li>
		<li>广州</li>
	</ul>
	<script type="text/javascript">
	    // 找到所有的li
	    var lis = document.getElementsByTagName("li");
	    var currentColor;
	    // 0 2  4
	    for(var i=0; i<lis.length; i++) {
	    	if (i%2 === 0) {
	    		lis[i].style.background = "pink";
	    	} else {
	    		lis[i].style.background = "orange";
	    	}
	    	// 给所有的li绑定鼠标移入事件
	    	lis[i].onmouseover = function() {
	    		// 记住当前元素背景色
	    		currentColor = this.style.background;
	    		// 鼠标放上去当前元素变红
	    		this.style.background = "red";
	    	}
	    	// 给所有的li绑定鼠标移走事件
	    	lis[i].onmouseout = function() {
	    		// 鼠标离开回复当前元素背景色
	    		this.style.background = currentColor;
	    	}
	    }
	</script>
</body>
</html>
```

6、其它js代码的书写位置

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
  <div onclick="alert(111);">123</div>	
  <script src="outer.js">
     // 这里引入了下面的外部js文件，此时不要写js代码
  </script>
  <script type="text/javascript">
     alert("ok");
  </script>
</body>
</html>
```

以下是outer.js文件内容

```js
alert("我是外部js");
```