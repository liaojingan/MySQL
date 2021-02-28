一、事件对象概念

    与事件相关的对象，事件（比如：鼠标单击、双击等）发生后，浏览器会传一个
    对象给事件处理函数，该对象封装了与该事件相关的信息（比如：clientX/clientY等可以在控制台查看）

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
    <script>
        document.onclick = function(e) {
            // 参数e与当前事件onclick鼠标事件有关
            alert(e);
        }
    </script>
</body>
</html>
```

二、兼容处理事件对象

    原则：先处理高级浏览器，后低级浏览器
    比如下面的e事件对象写在前面，先处理的高级浏览器，再加上event事件对象处理低级浏览器

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
    <script>
        document.onclick = function(e) {
            // 参数e与当前事件onclick鼠标事件有关
            var event_compatibility = e || event;
            console.log(event_compatibility);
        }
    </script>
</body>
</html>
```

三、事件对象常用的坐标属性

    screenX screenY 离电脑屏幕的距离
    clientX clientY 可视区域（就是文档页面可以看见的区域）
    pageX   pageY   以文档页面为准（加上滚动条不可见区域）——常用
    offsetX offsetY 相对于盒子的距离

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        /* 设置滚动条 */
        body {
            height: 2000px;
        }

        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }        
    </style>
</head>
<body>
    <div></div>
    <script>
        document.onclick = function(e) {
            // 先兼容处理
            var events = e || event;
            console.log(events.clientX + ":" + events.clientY);
            console.log(events.pageX + ":" + events.pageY);
            // console.log(events.screenX + ":" + events.screenY);
        }

        var oDiv = document.querySelector("div");
        oDiv.onmouseover = function(e) {
            var e = e || event;
            // 相对于盒子的距离
            console.log(e.offsetX + ":" + e.offsetY);
        }
    </script>
</body>
</html>
```

四、应用：图片跟随效果

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
            img {
                position: absolute;
            }
    </style>
</head>
<body>
    <img src="images/love.jpg" width="50" alt="">
    <script type="text/javascript">
        var oImg = document.querySelector("img");
        // 函数传入一个参数e，要用到坐标信息，因为信息是封装在这个事件对象里面
        // 注意是文档document绑定，不是图片img
        document.onmousemove  = function(e) {
            // 鼠标移动获取到位置进行移动，绑定鼠标移动事件
            // 先兼容
            var events = e || window.event;
            // 获取鼠标坐标
            var x = events.pageX;
            var y = events.pageY;
            // 鼠标坐标值减去对应的盒子的一半宽高
            // 宽度高度是元素固有的属性，所以可以直接(元素.属性)的方式调用，例如oImg.width
            oImg.style.left = x - oImg.width/2 + "px";
            oImg.style.top = y - oImg.height/2 + "px";
        }
    </script>
</body>
</html>
```

五、button属性（注意是属性不是元素）

    onmousedown 鼠标按下事件（左键、滚轮、右键）
    高版本谷歌、火狐、ie浏览器按下左键显示0，滚轮显示1，右键显示2
    对于ie8及以下浏览器 1 左键、4滚轮、2右键

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
    <script>
        document.onmousedown = function(e) {
            // 事件对象兼容，低版本只识别event
            // var e = e || event
            // 可以根据获取的数值来确定用户的行为是左击还是右击等
            // 获取到用户行为后，比如左击之后就做其它行为
            // alert(e.button);

            alert(getButton(e))
        }

        // 封装一个函数识别浏览器，e形参代表事件处理函数的形参
        function getButton(e) {
            // 能力检测
            if (e) {
                // 可以识别高版本浏览器，依然返回e.button
                return e.button;
                //如果识别到低版本，需要跟高版本统一
            } else if (window.event) {
                switch(event.button) {
                    case 1: return 0;
                    case 4: return 1;
                    case 2: return 2;
                }
            }
        }
    </script>
</body>
</html>
```

    字体图标网址：https://fontawesome.dashgame.com/  下载 解压
    查看网站如何使用字体图标

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <!-- 引入样式 -->
    <link rel="stylesheet" href="font-awsome/font-awesome-4.7.0/css/font-awesome.css">
</head>
    <style>
        div {
            top: 0;
            left: 0;
            color: green;
            font-size: 20px;    
            position: absolute;
        }
    </style>
<body>
    <div class="fa fa-leaf" style="left:340px;top:172px"></div>
    <div class="fa fa-leaf" style="left:172px;top:340px"></div>
    <div class="fa fa-leaf" style="left:69px;top:272px"></div>
    <div class="fa fa-leaf" style="left:69px;top:272px"></div>
    <div class="fa fa-leaf" style="left:75px;top:275px"></div>
    <div class="fa fa-leaf" style="left:77px;top:275px"></div>
    <div class="fa fa-leaf" style="left:83px;top:290px"></div>
    <div class="fa fa-leaf" style="left:340px;top:172px"></div>
    <div class="fa fa-leaf" style="left:85px;top:335px"></div>
    <div class="fa fa-leaf" style="left:85px;top:428px"></div>
    <div class="fa fa-leaf" style="left:75px;top:508px"></div>
    <div class="fa fa-leaf" style="left:78px;top:172px"></div>
    <script> 
        var divs = document.querySelectorAll("div");
        // 这里是在文档的任意位置都可以触发事件，而不仅仅是在div盒子中
        // 所以是document.onmousemove 而不是divs.onmousemove
        document.onmousemove = function(e) {
            var e = e || event;
            // 设置第一个叶子的位置是鼠标位置
            divs[0].style.left = e.pageX + "px";
            divs[0].style.top = e.pageY + "px";
            for(var i=divs.length-1; i>0; i--) {
                divs[i].style.left = divs[i-1].style.left;
                divs[i].style.top = divs[i-1].style.top;
            }
        }
    </script>
</body>
</html>
```

键盘事件

        键盘按键值的问题
        onkeydown键盘按下、 onkeyup键盘弹起、 onkeyperss键盘按下过程中

        e.keyCode 表示按下不同按键返回不同值的属性（注意：无论大小写字母都是一样按照大写的ASCII值，也就是说
        按下A和a的按键的值是一样的，都是65）

        封装的特殊属性，主要是ctrl这样的控制键
        例如ctrlKey属性：表示有没有按下ctrl键——》如果有返回true，没有返回false
        altKey、shiftKey等属性 ：表示有没有按下alt键

        还可以使用的场景：比如在键盘按下A就在网页显示酷炫字体A等

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
    <script>
        document.onkeydown = function(e) {
            var e = e || event;
            // e.keyCode属性，表示按下不同的键，键盘值是不一样的
            // console.log(e.keyCode);
            console.log(e.ctrlKey);
        }
    </script>
</body>
</html>
```

应用

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
    <script>
        document.onkeypress = function(e) {
            var e = e || event;
            console.log(e.keyCode);
            // ctrl——》13 和ctrl+enter——》10 按下ctrl或者ctrl+enter同时按下发送消息
            // 但是按下shift+enter也是13

            // 必须按下ctrl+enter才能发送消息
            if (e.ctrlKey && e.keyCode == 10) {
                alert("发送");
            }
        }
    </script>
</body>
</html>
```

事件冒泡

    所有事件当中，如果没有阻止事件冒泡，执行当中的某一个事件后，会自动冒泡往上继续执行其它事件
    事件执行冒泡顺序：body元素、body、document、window

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
        .fa {
            width: 300px;
            height: 300px;
            background-color: pink;
        }

        .son {
            width: 100px;
            height: 100px;
            background-color: skyblue;
        }
    </style>
<body>
    <div class="fa">
        <div class="son"></div>
    </div>
    <script>
            // querySelector 高版本才支持
            var fa = document.querySelector(".fa");
            var son = document.querySelector(".son");
            // 给父亲和儿子元素、document都绑定事件
            // 然后执行程序点击儿子盒子发现先执行son事件，然后接着自动执行fa事件
            fa.onclick = function() {
                alert("fa");
            }

            son.onclick = function() {
                alert("son");s
            }

            document.onclick = function() {
                alert("document");
            }

            window.onclick = function() {
                alert("window");
            }
    </script>
</body>
</html>
```

    浏览器默认行为阻止事件冒泡
    （1）e.stopPropagation();  此方法IE浏览器不支持
    （2）e.cancelBubble = true 此属性支持IE浏览器，默认是false，为true时表示阻止冒泡

    兼容检测：先查找这个对象是否有这个属性(e.stopPropagation)，如果有就调用此方法[e.stopPropagation()]
    如果不支持就用这个属性并把值设置成true(e.cancelBubble = true)

    至于需不需要用到阻止冒泡，具体看业务逻辑

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
        .fa {
            width: 300px;
            height: 300px;
            background-color: pink;
        }

        .son {
            width: 100px;
            height: 100px;
            background-color: skyblue;
        }
    </style>
<body>
    <div class="fa">
        <div class="son"></div>
    </div>
    <script>
            // IE8以上才支持querySelector
            var fa = document.querySelector(".fa");
            var son = document.querySelector(".son");
            // 给父亲和儿子元素、document都绑定事件
            // 然后执行程序点击儿子盒子发现先执行son事件，然后接着自动执行fa事件
            fa.onclick = function() {
                alert("fa");
            }

            son.onclick = function() {
                alert("son");s
            }

            document.onclick = function(e) {
                // 阻止冒泡,执行完document这个事件就不会再往下执行了
                // e.stopPropagation();  兼容处理
                // e.cancelBubble 这个属性支持IE
                e.stopPropagation?e.stopPropagation():e.cancelBubble = true;
                alert("document");
            }

            window.onclick = function() {
                alert("window");
            }
    </script>
</body>
</html>
```

应用

    弹出个人信息：点击按钮显示个人信息列表，点击文档其它位置就隐藏列表
    下面的第一个例子效果是：点击按钮后列表隐藏了，点击其它位置无反应，原因是执行完点击按钮事件后
    紧接着事件冒泡，执行document事件把列表给隐藏了，所以需要阻止冒泡事件

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
    <button>显示个人信息</button>
    <ul>
        <li>姓名：珍珍</li>
        <li>年龄：24</li>
        <li>性别：女</li>
    </ul>
    <script>
        var btn = document.getElementsByTagName("button")[0];
        var getUl = document.getElementsByTagName("ul")[0];

        btn.onclick = function() {
            getUl.style.display = "block";
        }

        // 点击文档的其它位置隐藏列表，所以绑定document
        document.onclick = function() {
            getUl.style.display = "none";
        }
    </script>
</body>
</html>
```

    阻止冒泡

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
    <button>显示个人信息</button>
    <ul>
        <li>姓名：珍珍</li>
        <li>年龄：24</li>
        <li>性别：女</li>
    </ul>
    <script>
        var btn = document.getElementsByTagName("button")[0];
        var getUl = document.getElementsByTagName("ul")[0];

        btn.onclick = function(e) {
            // 阻止冒泡
            e.stopPropagation?e.stopPropagation():e.cancelBubble=true;
            getUl.style.display = "block";
        }

        // 点击文档的其它位置隐藏列表，所以绑定document
        document.onclick = function() {
            getUl.style.display = "none";
        }
    </script>
</body>
</html>
```

阻止浏览器的默认行为

    例如：链接，当点击链接后就跳转，这就是浏览器的默认行为
    当需要点击这个链接做其它事情（弹窗）就是阻止了默认行为

    阻止默认行为的方式：
    1、加上return false; （常用）
    2、e.preventDefault();适用于高版本浏览器
    3、e.returnValue = false;适用于低版本浏览器

    兼容处理：先判断是否有这个方法,有就调用
    e.preventDefault?e.preventDefault():e.returnValue = false;

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
    <div></div>
    <a href="http://www.163.com">网易</a>
    <script>
        var alink = document.querySelector("a");
        alink.onclick = function() {
            alert("success");
            // 要想点击a链接执行弹窗事件后不再默认跳转到网易页
            return false;  // 阻止默认行为
        }
    </script>
</body>
</html>
```

应用

    整个文档中右击鼠标出来图片，本身默认行为是右击鼠标出来菜单
    oncontextmenu鼠标右击事件
