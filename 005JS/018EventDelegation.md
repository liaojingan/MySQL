1、animate.css动画库网站

    http://www.jq22.com/yanshi819/ 可以直接在上面下载样式使用

    键盘值应用：打开一个页面随机产生一个字母，然后键盘上按下字母，如果跟随机产生的字母
    一致就显示当前颜色，如果不一致显示红色，并且统计正确率

    以下应用先下载对应的animate.css到对应的文件中

```html
<html>
    <head>
        <meta charset="utf-8">
        <title>打字游戏</title>
        <!--引入animate.css动画库-->
        <link rel="stylesheet" href="animate.css">
        <style>
            body{
                margin: 0;
                /*开启弹性布局，并让弹性布局中的子元素
                水平居中对齐，垂直居中对齐*/
                display: flex;
                justify-content: center;
                align-items: center;
                /*文字居中*/
                text-align: center;
                /*设置背景颜色的经像渐变*/
                background: radial-gradient(circle,#444,#111,#000);
            }
            #char{
                font-size: 400px;
                color: lightgreen;
                /*设置文字阴影*/
                /*text-shadow: 水平位置 垂直位置 模糊距离 阴影颜色*/
                /*位置可以为负值*/
                text-shadow: 0 0 50px #666;
            }
            #result{
                font-size: 20px;
                color: #888;
            }
            /*找到id为char及类名为error的div元素*/
            #char.error{
                color: red;

            }
        </style>
    </head>
    <body>
        <main>
            <div id="char">A</div>
            <div id="result">请在按键上按下屏幕上显示的字母</div>
        </main>
    </body>
</html>
<script>
    // animated为最基础的效果，无论调用动画库里的哪个效果都要先添加，后面再添加其他类作为效果
	// 按键正确加入样式也就是调用动画库里的css： "animated zoomIn";
	// 按键错误加入样式： "animated shake error";
    // 页面加载  char中随机显示 A--Z之间的任意一个字符   65 --- += "错误" + errorCount + "个";
    // 随机产生A-Z  65-90 

    function rand(min,max) {
        // 保证调用时输入的实参第一个数小于第二个数
        if (min > max) {
            var t = min;
            min = max;
            max = t;                                                                                                                                            
        }
        return parseInt(Math.random()*(max-min+1)+min);
        //65<=Math.random()*26+65<26+65   注意return是放在函数外面
    }

    // 找元素
    function $(id) {
        // 注意：一定要添加return
        return document.getElementById(id);
    }

    // 打开页面让div随机产生一个字母
    // 定义一个全局变量var code，因为后面判断字符跟keyCode是否一致也需要用到
    // 所以全局变量后面调用的时候就不用加code了
    var code = null;
    function showChar() {
        // 思路：随机产生一个65-90数值，之后拿到对应的字符
        // 不管大小写，都会自动按照大写返回
        // 不用加var 因为code已经是全局变量
        code = rand(65,90);
        var ch = String.fromCharCode(code);
        $("char").innerHTML = ch;
    }
    showChar()

    // 定义变量
    var correct = 0;
    var errorNum = 0;
    document.onkeydown = function(e) {
        var e = e || event;
        // 如果e.keyCode键盘字符与随机字符相等正确数加1,且增加改变类的样式
        if(e.keyCode === code) {
            correct++;
            $("char").className = "animated zoomIn";
            showChar();
        } else {
            errorNum++;
            $("char").className = "animated shake error";
            showChar();
        }

        // 经过一段时间需要清空动画，不然第二次点击没有效果展示
        setTimeout(function() {
            $("char").className = "";
        }, 500);
        // 清空动画后，调用统计的函数统计正确率
        count();
    }

    function count() {
        // toFixed表示保留几位小数
        var res = 100*(correct/(correct+errorNum).toFixed(2));
        $("result").innerHTML = "正确率" + res + "%";
    }
</script>
```

事件委托（事件代理）

    利用事件冒泡传播机制
    比如：ul下的li元素列表，要想实现点击列表中的每个li元素都弹出弹窗
    不需要绑定每个li元素，只需要绑定ul即可，因为事件冒泡的原因，点击
    li元素执行事件后，会继续冒泡执行ul事件

    相比之下好处：
    一、使用事件冒泡机制性能较好，元素越多性能越好；
    二、使用事件代理机制新增的动态元素，之前点击li元素弹出弹窗的事件依然有效，但是if绑定的则无效


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
    <ul>
        <li>111</li>
        <li>222</li>
        <li>333</li>
        <li>444</li>
        <li>555</li>
    </ul>
    <script>
        // 不使用事件冒泡实现点击每个Li元素弹出弹窗效果
        // 这种方式找元素和绑定元素都要消耗性能
        var lis = document.querySelectorAll("li");
        for(var i=0; i<lis.length; i++) {
            // 注意不要缺少[i]
            lis[i].onclick = function() {
                alert("弹窗");
            }
        }
    </script>
</body>
</html>
```

 target获取当前事件源

    获取当前事件源后，实现点击不同的li元素，表现不同的逻辑

```html
<body>
    <ul>
        <li>111</li>
        <li>222</li>
        <li>333</li>
        <li>444</li>
        <li>555</li>
    </ul>
    <script>
        var getUl = document.querySelector("ul");
        getUl.onclick = function(e) {
            // 点击li元素后获取当前事件源，例如点击第一li就返回事件源<li>111</li>
            console.log(e.target); 
        }
    </script>
</body>
```

    兼容处理获取事件源

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
    <ul>
        <li id="one">111</li>
        <li>222</li>
        <li>333</li>
        <li>444</li>
        <li>555</li>
    </ul>
    <script>
        var getUl = document.querySelector("ul");
        getUl.onclick = function(e) {
            // 先兼容e
            var e = e || event;
            var target = e.target || e.srcElement // e.srcElement兼容低版本
            if (e.target.id == "one") {
                alert("第一个Li");
            }
        }
    </script>
</body>
</html>
```

应用

        实现点击按钮新增li元素，然后添加到列表中

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
    <button>新增li</button>
    <ul>
        <li id="one">111</li>
        <li>222</li>
        <li>333</li>
        <li>444</li>
        <li>555</li>
    </ul>
    <script>
        var btn = document.querySelector("button");
        var getUl = document.querySelector("ul");

        getUl.onclick = function(e) {
            var e = e || event;
            var target = e.target || e.srcElement;
            console.log(e.target.innerHTML);
        }
        btn.onclick = function(e) {
            var createLi = document.createElement("li");
            // 新增加的动态元素依然会执行上面点击li元素获取事件源的操作
            // 使用事件代理机制，动态添加的元素可以有效执行上面的操作，如果是用if循环绑定的元素则不可以
            createLi.innerHTML = "动态添加666";
            getUl.appendChild(createLi);
        }
    </script>
</body>
</html>
```


事件传播完整机制经历的阶段

    分为三个阶段：
    先从左边，最外面的widonw开始往下找，这个第一阶段叫“捕获”阶段
    接下来第二个阶段为：目标阶段（比如找到fa）
    然后从左边往上开始冒泡，这个第三阶段叫“冒泡”阶段

    window         window         
    document       document
    html           html
    body           body
    fa             fa
    son            son

    DOM0级事件绑定的方法都是在当前元素事件行为的冒泡阶段执行
    通俗来讲就是，当你点击fa元素，fa元素先出来，就是第一个找到目标先出来，然后往上冒泡执行

DOM0级应用


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

        .fa .son {
            width: 200px;
            height: 200px;
            background-color: skyblue;
        }
    </style>
<body>
    <div class="fa">
        <div class="son"></div>
    </div>
    <script>
        // querySelector里面是填写类名
        var fa = document.querySelector(".fa");
        var son = document.querySelector(".son");
        window.onclick = function() {
            console.log("window");
        }
        
        document.onclick = function() {
            console.log("document");
        }

        // documentElement表示html
         document.documentElement.onclick = function() {
            console.log("html");
        }

        document.body.onclick = function() {
            console.log("body");
        }

        fa.onclick = function() {
            console.log("fa");
        }

        son.onclick = function() {
            console.log("son");  
        }
    </script>
</body>
</html>
```

DOM2级绑定事件

    addEventListener(event,listener,useCapture)  
    注意：event事件名称——》例如DOM0级用onclick,在DOM2级用click即可
          useCapture默认是false

    addEventListener(事件名称,事件回调函数,是否捕获)
    要想显示先捕获则把useCapture设置为true


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

        .fa .son {
            width: 200px;
            height: 200px;
            background-color: skyblue;
        }
    </style>
<body>
    <div class="fa">
        <div class="son"></div>
    </div>
    <script>
        var fa = document.querySelector(".fa");

        window.addEventListener("click",function() {
            console.log("window 捕获");
        },true);

        window.addEventListener("click",function() {
            console.log("window 冒泡");
        },false);

        document.addEventListener("click",function() {
            console.log("document 捕获");
        },true);

        document.addEventListener("click",function() {
            console.log("document 冒泡");
        },false);

        document.body.addEventListener("click",function() {
            console.log("body 捕获");
        },true);

        document.body.addEventListener("click",function() {
            console.log("body 冒泡");
        },false);

        fa.addEventListener("click",function() {
            console.log("fa 捕获");
        },true);

        fa.addEventListener("click",function() {
            console.log("fa 冒泡");
        },false);
    </script>
</body>
</html>
```


    捕获作为了解，主要是冒泡

    操作触发某一个用户的行为
    例如：点击fa元素，执行了这个事件方法，此时浏览器会把存储的对象，传给每一个执行的方法
    点击fa元素，这个封装的对象就跟fa相关，然后冒泡，就会把fa相关的事件对象继续传递


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

        .fa .son {
            width: 200px;
            height: 200px;
            background-color: skyblue;
        }
    </style>
<body>
    <div class="fa">
        <div class="son"></div>
    </div>
    <script>
        var fa = document.querySelector(".fa");

        window.addEventListener("click",function(e) {
            console.log(e == myEvent);
        },false);

        document.addEventListener("click",function(e) {
            console.log(e == myEvent);
        },false);

        document.body.addEventListener("click",function(e) {
            console.log(e == myEvent);
        },false);

        fa.addEventListener("click",function(e) {
            console.log("fa 冒泡");
            myEvent = e;
        },false);
    </script>
</body>
</html>
```

IE高版本完整机制

    window html body

IE低版本完整机制

    html body

谷歌完整机制

    window document html body fa son



