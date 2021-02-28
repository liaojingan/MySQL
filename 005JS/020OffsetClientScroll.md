js盒模型属性

    client
        width/height/top/left
        clientWidth padding+width
        clientLeft 左边框宽度

    offset
        offsetWidth  padding+width+border
        offsetParent     

    scroll
        scrollWidth 左border+内容真实宽
        scrollHeight 上border+内容真实高

   offsetLeft/offsetTop  offsetParent

   offsetLeft 指的是元素与offsetParent之间的距离(参考点offsetParent)

   首先确定offsetParent参考点
      IE8+和高级浏览器
          假如祖先元素中都没有定位（绝对、固定、相对定位），offsetParent就是body元素,假如祖先元素有定位，则以最近的带有定位的祖先元素为准,与自己是否定位无关
      vue最低兼容到IE8，所以用了vue就兼容不到

      IE6/7浏览器
          自身没有定位，参考的是最近的有宽高的祖先元素，没有宽高参考的是body
          自身有定位 与高级浏览器一致

    offsetLeft 
        IE9+和高级浏览器，IE6/7
        元素自身的左边框外部到offsetParent左边框内部的距离 

        IE8 
        比高版本浏览器的offsetLeft多一个offsetParent边框   

    如何对offsetLeft做兼容？
          自身元素定位  祖先无边框        

==========================================


    确定offsetParent参考点
    IE8+和高级浏览器
    假如祖先元素中都没有定位（绝对、固定、相对定位），offsetParent就是body元素


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .box1 {
            width: 400px;
            height: 400px;
            padding: 50px;
            border: 10px solid red;
        }

        .box2 {
            width: 260px;
            height: 260px;
            padding: 50px;
            border: 10px solid green;
        }

        .box3 {
            width: 160px;
            height: 160px;
            padding: 50px;
            border: 10px solid blue;
        }

        #op {
            width: 80px;
            height: 80px;
            border: 20px solid purple;
        }
    </style>
<body>
    <div class="box1">
        <div class="box2">
            <div class="box3">
                <p id="op"></p>
            </div>
        </div>
    </div>
    <script>
        var op = document.getElementById("op");
        alert(op.offsetParent); // HTMLBody
    </script>
</body>
</html>
```

    假如祖先元素有定位，则以最近的带有定位的祖先元素为准,与自己是否定位无关


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .box1 {
            width: 400px;
            height: 400px;
            padding: 50px;
            border: 10px solid red;
        }

        .box2 {
            width: 260px;
            height: 260px;
            padding: 50px;
            position: relative;
            border: 10px solid green;
        }

        .box3 {
            width: 160px;
            height: 160px;
            padding: 50px;
            position: relative;
            border: 10px solid blue;
        }

        #op {
            width: 80px;
            height: 80px;
            border: 20px solid purple;
            position: relative;
        }
    </style>
<body>
    <div class="box1">
        <div class="box2">
            <div class="box3">
                <p id="op"></p>
            </div>
        </div>
    </div>
    <script>
        var op = document.getElementById("op");
        alert(op.offsetParent); // HTMLDivElement
        // 如果p元素的父亲和爷爷元素都有定位，则以最近带有定位的祖先元素为准
        alert(op.offsetParent.className) // box3
    </script>
</body>
</html>
```

    offsetLeft 
        IE9+和高级浏览器，IE6/7
        元素自身的左边框外部到offsetParent左边框内部的距离
        下图示例其余元素都未设置定位

    offsetTop是类似于offsetLeft


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .box1 {
            width: 400px;
            height: 400px;
            padding: 50px;
            border: 10px solid red;
        }

        .box2 {
            width: 260px;
            height: 260px;
            padding: 50px;
            border: 10px solid green;
        }

        .box3 {
            width: 160px;
            height: 160px;
            padding: 50px;
            border: 10px solid blue;
        }

        #op {
            width: 80px;
            height: 80px;
            border: 20px solid purple;
            position: relative;
        }
    </style>
<body>
    <div class="box1">
        <div class="box2">
            <div class="box3">
                <p id="op"></p>
            </div>
        </div>
    </div>
    <script>
        var op = document.getElementById("op");
        alert(op.offsetParent);
    </script>
</body>
</html>
```

![offsetLeft](../picture/offsetLeft.png)

    了解这些原生底层，后面jquery都有

scrollTop、scrollLeft

    常用来计算窗口向上卷动的距离是多少

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style type="text/css">
	     body {
	     	height: 2000px;
	     }
	</style>
</head>
<body>
	
	<script type="text/javascript">
	      // 卷动事件
          onscroll = function() {
              // 计算被卷（看不见）的距离 高版本
          	  // console.log(document.documentElement.scrollTop); 
          	  // console.log(document.body.scrollTop);
              // 兼容处理
          	  var scrollTop = document.documentElement.scrollTop || doucument.body.scrollTop;
          } 
	</script>
</body>
</html>
```


应用

    向下滑动窗口出现小火箭图标，点击图片图片卷动到顶部


```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        body {
            height: 2000px;
        }

       .top{
           /* 固定定位 */
           position: fixed;
           right:50px;
           bottom:100px;
           display: none;
       }

    </style>
     
    
</head>
<body>
<div id="gotop" class="top">
    <img src="images/Top.jpg" alt=""/>
</div>
 <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
   <p>天王盖地虎，小鸡炖蘑菇</p>
</body>
</html>
<script type="text/javascript">
    var gotop = document.getElementById("gotop");
    // 获取滚动条向上滑动被卷的距离
    onscroll = function() {
        var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
        if (scrollTop>0) {
            gotop.style.display = "block";
        } else {
            gotop.style.display = "none";
        }
    }

    gotop.onclick = function() {
        document.documentElement.scrollTop = 0;
    }
</script>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style type="text/css">
	   .progress {
	   	   margin: auto;
	   	   width: 200px;
	   	   height: 20px;
	   	   border: thin dotted darkgreen;
           /* 需要填充，使用定位 */
	   	   position: relative;
	   	   top: 200px;
	   }

	   .fillDiv {
	   	   position: absolute;
	   	   left: 0;
	   	   top: 0;
           /* 默认进度条进度为0% */
	   	   width: 0px;
	   	   height: 20px;
	   	   background-color: red;
	   }

	   #percent {
           /* 定位百分比数值在边框最右边 */
	   	   position: absolute;
	   	   left: 206px;
	   	   top: 0;
	   }
	</style>
</head>
<body>
	<div class="progress" id="progress">
		<div class="fillDiv" id="fillDiv"></div>
		<span id="percent">0</span>
	</div>
    <script type="text/javascript">
        // 思路  使用定时器每隔一段时间不断改变fillDiv的宽度
        function $(id) {
        	return document.getElementById(id);
        }  

        // 设置一个变量存储定时时，当进度条为100%时需要停止
        var timer = setInterval(function() {
            // 获取填充的宽度
             $("fillDiv").style.width = $("fillDiv").clientWidth + 2 + "px"; 
             // 获取数值百分比（动态获取的宽度/总宽度 = 进度百分比）
             var percent = parseInt(100*($("fillDiv").clientWidth / $("progress").clientWidth)) + "%";
             $("percent").innerHTML = percent;
             // 取消定时器
             if (fillDiv.clientWidth >= 200) {
             	clearInterval(timer);
             }  
        }, 10);
    </script>
</body>
</html>
```

    模拟垂直滚动条
    比例问题：滚动条拉动到底部，内容也要卷动到最底部

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box {
            width: 300px;
            height: 500px;
            border: 1px solid red;
            margin:100px;
            position: relative;
        }
        .content {
            height: auto;
            padding: 5px 18px 5px 5px;
            position: absolute;
            top: 0;
            left: 0;
        }
        .scroll {
            width: 18px;
            height: 100%;
            position: absolute;
            top: 0;
            right: 0;
            background-color: #eee;
        }
        .bar {
            width: 100%;
            height: 100px;
            background-color: red;
            cursor: pointer;
            border-radius: 10px;
            position: absolute;
            top: 0;
            left: 0;
        }
    </style>
</head>
<body>
<div class="box" id="box"><!--内容可视区-->
    <div id="content" class="content" ><!--内容区-->
     你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的
	 小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你
	 是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小
	 苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果 
	 你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的
	 小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你
	 是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小
	 苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果 
	 你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的
	 小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你
	 是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小
	 苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果 
	 你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的
	 小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你
	 是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小
	 苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果 
	 你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的
	 小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你
	 是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小
	 苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果你是我的小苹果 
    </div>
    <div id="scroll" class="scroll"><!--滚动条所在区域-->
        <div id="bar" class="bar"></div><!--滚动条-->
    </div>
</div>
<script type="text/javascript">
      function $(id) {
            return document.getElementById(id);
      }

      var box = $("box");
      var content = $("content");
      var bar = $("bar");
      // 鼠标按下再进行拖动事件（拖拽事件）
      bar.onmousedown = function(e) {
          var e = e || window.event; 
          //console.log(e.offsetY); 
          // 滚动条自身点击到盒子顶部距离 + 盒子上边框外部到offsetParent(body)上边框内部距离
          var dis = e.offsetY + box.offsetTop;
          // 上面按下鼠标事件，这里是按下后拖动滚动条事件
          document.onmousemove = function(e) {
              var e = e || window.event; 
              var y = e.pageY - dis;
              // 最大移动距离
              var maxT = box.offsetHeight - bar.offsetHeight;
              if (y<0) {
                 y = 0;
              } else if (y>maxT) {
                 y = maxT;
              }
              bar.style.top = y + "px";
              // 内容向上走的距离 / 滚动条向下的距离 = 内容高度-可视区域高度 / 滚动条向下最大距离
              var t = (content.offsetHeight-box.offsetHeight)*y/maxT;
              // 往上走所以是负值
              content.style.top = -t + "px";
          } 

          // 鼠标在滚动条上弹起时取消拖拽事件
          document.onmouseup = function() {
              document.onmousemove = null;
          }   
          return false;
      } 

        
</script>
</body>
</html>
```

