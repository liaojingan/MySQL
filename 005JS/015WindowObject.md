一、window对象

    （1）可在控制台输入：window 就会显示大部分对象
    例如：window.alert("ok"),其中window可以省略

    控制台输入window可查看

    （2）定义的全局变量会挂载到window的对象下
    （3）定义的全局函数同样也会

```html
<script>
    var d = 100;
    alert(d);
    // alert(window.d) 跟上面的效果一致

    function fn() {
        alert(3);
    }
    fn()
    // window.fn() 跟上面效果一致
</script>
```


二、常用window对象

    弹窗：confirm() prompt() alert()
    定时器:setTimeout 每隔一段时间，执行某个函数的操作（不会重复执行，只执行一次操作）

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
        // 隔一秒钟显示i的值，时间的单位是毫秒，此例子为匿名函数也是函数
        var i = 0;
        window.setTimeout(function(){
            document.write(i);
        },1000)
    </script>
</body>
</html>
```

    清除和取消定时广告实例

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
    <button id="btn">清除广告</button>
    <button id="btnStop">取消</button>
    <img id="pic" src="picture/hua1.jpg" alt="花盆">

    <script>
        var btn = document.getElementById("btn");
        var get_img = document.getElementById("pic");
        // querySelector里面写的是css属性值
        var btnStop = document.querySelector("#btnStop")
        // 设置一个全局的变量timer，单击清除广告按钮时记住当前状态，单击取消就清除这个状态；
        // 不可设置为局部变量，因为不止绑定清除广告事件需要调用，取消绑定事件也需要使用
        var timer = null;
        btn.onclick = function() {
            // 记住这个状态
            timer = setTimeout(function() {
                get_img.style.display = "none";
            },3000);
        }

        // 取消绑定事件
        btnStop.onclick = function() {
            // 清除上面保存的状态
            clearTimeout(timer)
        }
        
    </script>
</body>
</html>
```

三、定时器异步问题

    异步：事件回调、定时器、ajax、node（绝大部分是异步的）效率比同步高
    遇到耗时的实践，不必一直等下去，可以先执行其它事件再回来（好比餐厅来了两桌客人，只有一个服务员，可以先给菜单给一桌人，不用等他们点完菜；直接先去服务另一桌人，）

    同步：只能前面一件事执行完，再执行下一件事情（遇到耗时的事件，必须等到做完才可以往下走，就好像服务员必须等到客人点完菜，才能把菜单送到后厨）   

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
       var i = 10;
       setTimeout(function() {
           i += 5;
           console.log(i);
       }, 1000);
    //    执行代码的时候遇到setTimeout异步任务需要排队，跟上面的1000毫秒无关，
    //    可以设置为0；需要排队，然后线程先执行下面剩下的，然后再回来执行队列里的异步任务

    //    异步的任务哪怕时间设置为0毫秒也不能立刻执行，必须等同步的做完了才可以回来执行
    //    跟时间无关。

    //    后面有很多同步的也需要先全部执行完，才能回去执行异步的
       console.log(i);
       console.log("ok");
       console.log("nice");
    </script>
</body>
</html>
```

四、location对象（例如：用于网页定时跳转）

    在控制台输入：location可以看到href网页地址

```html
<script>
console.log(location)
</script>
```


    可用这个登录地址来跳转地址，比如修改href地址来跳转访问网易

 ```html
<script>
location.href = "http://www.163.com";
</script>
```  

    设置三秒后定时任务打开网易

 ```html
<script>
    setTimeout(function() {
        location.href = "http://www.163.com";
    }, 3000);
</script>
``` 

    使用replace()不能后退到上一级页面，没有保留上一次页面

```html
    <script>
        setTimeout(function() {
            location.replace("http://www.163.com")
        }, 3000);
    </script>
```

    使用assign()可以后退到上一级页面

```html
    <script>
        setTimeout(function() {
            location.assign("http://www.163.com");
        }, 3000);
    </script>
```

    使用history保存历史记录来操作页面的前进后退
    例如下面建立a.html和b.htm两个页面

```html
<!-- a页面 -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- <button onclick="location.href='b.html'">跳转b页面</button> -->
    <button id="btn">跳转到b页面</button>
    <button onclick="history.go(1)">前进</button>
    <script>
        // 也可直接使用上面行内样式，不用绑定事件，因为代码比较简单
        var btn = document.getElementById("btn");
        btn.onclick = function() {
            location.href = "b.html";
        }
    </script>
</body>
</html>
```

```html
<!-- b页面 -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- a页面跳转到b页面后，点击b页面按钮回到a页面 -->
    <!-- window有个对象history可以保存从a跳转b页面的历史记录，这样b页面就加载到记录里面了
    如果要后退加上go(-1),其中-1表示回到上一级 -->
    <button onclick="history.go(-1)">后退到a</button>
</body>
</html>
```


