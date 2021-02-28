应用

    放大镜：移动遮罩层放大图片

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<style type="text/css">
		*{
			margin: 0;
			padding: 0;
		}
		#box{
			width: 350px;
			height: 350px;
			border: 1px solid #000;
			margin: 200px;
			position: relative;
		}
		#big{
			width: 400px;
			height: 400px;
			border: 1px solid #000;
			overflow: hidden;
			position: absolute;
			top:0;
			left : 360px;
			display: none;
		}
		#mask{
			width: 175px;
			height: 175px;
			background: paleturquoise;
			position: absolute;
			left:0;
			top: 0;
			opacity: 0.3;
			display: none;
			cursor: move;
		}
		#small{
			position: relative;
		}
		#bigImg{
			position: absolute;
			left: 0;
			top: 0;
		}
	</style>
	<body>
		<div id="box" >
			<div id="small"><!--小图区-->
				<img src="01放大镜/001.jpg" alt="" />
				<div id="mask"></div><!--遮罩层-->
			</div>
			<div id="big"><!--大图区-->
				<img src="01放大镜/0001.jpg" alt="" id="bigImg"/>
			</div>
		</div>
	</body>
</html>
<script type="text/javascript">
	 function $(id) {
		 return document.getElementById(id);
	 }
     
	 var box = $("box");
	 var small = $("small");
	 var mask = $("mask");
	 var big = $("big");
	 var bigImg = $("bigImg");
	 // 鼠标移入到小图区域 mask和big显示
	 small.onmouseover = function() {
		 mask.style.display = "block";
		 big.style.display = "block";
	 } 
	 // 鼠标移出小图区域 mask和big隐藏
	 small.onmouseout = function() {
		 mask.style.display = "none";
		 big.style.display = "none";
	 } 
	 // 鼠标在小图区域移动 让mask移动
	 small.onmousemove = function(e) {
        var e = e || window.event;
		var x = e.pageX - box.offsetLeft - mask.offsetWidth/2;
		var y = e.pageY - box.offsetTop - mask.offsetHeight/2;
        // 得到mask位置最大值
		var maxX = box.clientWidth - mask.clientWidth;
		var maxY = box.clientHeight - mask.clientHeight;

		// 注意需要赋值给x、y
		x = x < 0? 0: (x > maxX ? maxX : x);
		y = y < 0? 0: (y > maxY ? maxY : y);

		// 注意加上单位
		mask.style.left = x + "px";
		mask.style.top = y + "px";

		// 小图片宽度：大图片宽度 = x: 大图片位置 （x表示遮罩层移动的距离）
		// 因为移动鼠标向左移动，那么大图就要向右才能查看，所以需要加上负号
		var bigImgLeft = -x*bigImg.offsetWidth/small.offsetWidth;
		var bigImgTop = -y*bigImg.offsetHeight/small.offsetHeight;
		// 设置大图片移动位置
		bigImg.style.left = bigImgLeft + "px";
		bigImg.style.top = bigImgTop + "px";
	 }
</script>
```


    吸顶效果

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        *{margin:0;padding:0}
        img{
            vertical-align: top;
        }
		.top img{
			height:168px;
		}
        .main{
            margin:0 auto;
            width:1000px;
            margin-top:10px;

        }
		
    </style>
</head>
<body>
	<div class="top" id="top">
	    <img src="images/top.png" alt="" id="topImg"/>
	</div>
	<div class="nav" id="Q-nav">
	    <img src="images/nav.png" alt=""/>
	</div>
	<div class="main">
	    <img src="images/main.png" alt=""/>
	</div>
</body>
</html>
<script type="text/javascript">
     function $(id) {
		 return document.getElementById(id);
	 }
     // 页面滚走的距离正好是头部的距离 让nav采用固定定位
	 // 动态获取图片头部高度可以用height,如果不是图片可以使用offsetHeight等
	 var h = $("topImg").height;
	 onscroll = function() {
		 var sTop = document.documentElement.scrollTop || document.body.scrollTop;
		 if (sTop >= h) {
			 $("Q-nav").style.position = "fixed";
			 $("Q-nav").style.top = 0;
			 $("Q-nav").style.left = 0;
			 // 一定要写否则，写会造成只有第一次生效，再往上滑动滚动条时头部依然处于固定定位，需要取消
		 } else {
			 $("Q-nav").style.position = "";
		 }
	 }
</script>	
 ```


    无缝滚动

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        div {
            width: 600px;
            height: 200px;
            margin: 100px;
            overflow: hidden;
            position: relative;
            border: 1px solid red;
        }

        ul {
            width: 600%;
            position: absolute;
            left: 0;
        }

        li {
            float: left;
            list-style: none;
        }
    </style>
</head>
<body>
    <div id="box">
        <ul id="u">
            <li><img src="images/a.jpg" alt=""></li>
            <li><img src="images/b.jpg" alt=""></li>
            <li><img src="images/d.jpg" alt=""></li>
            <li><img src="images/a.jpg" alt=""></li>
            <li><img src="images/b.jpg" alt=""></li>
            <li><img src="images/d.jpg" alt=""></li>
        </ul>
    </div>
</body>
</html>
<script>
    var num = 0; // 默认ul位置
    var getUl = document.getElementById("u");
    var box = document.getElementById("box");

    function autoplay() {
        // 设置让left的值不断减小
        getUl.style.left = num + "px";
        // 图片不断向左移动，所以用负数
        num -= 2;   
        // num值先设置将所有图片移除，然后就会默认显示多添加的图片，这个时候重置为0
        if(num <= -900) {
            num = 0;
        }
    }
    // 启动定时器
    var timer = setInterval(autoplay,20);

    // 鼠标放在图片上，不滚动
    box.onmouseover = function() {
        clearInterval(timer);
    }

    // 鼠标离开图片，再次滚动

    box.onmouseout = function() {
        // 注意需要再次赋值给timer，才会启用
        timer = setInterval(autoplay,20);
    }
</script>
```

