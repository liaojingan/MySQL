一、window对象setInterval异步定时器


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
        // 每隔一段时间就执行一段代码一次 全称window.setInterval
        // 语法与setTimeout类似，经过几秒就执行一段代码，但这个对象重复执行
        // 函数作为参数传给另一个函数叫高阶函数

        setInterval(function() {
            alert("每隔两秒就弹窗一次");
        }, 2000);

        // 其它方式使用，逻辑较复杂使用下面的方面
        // 先将要执行操作的函数放到外面
        function fn() {
            alert("每隔两秒就弹窗一次");
        }
        // 再将上面定义好的函数名传入定时器函数
        // 注意传入下面定时器的是函数fn，而不是fn()
        // fn()这种叫做函数的调用，最后会得到一个返回值传到定时器
        // 上面函数没有返回值，就会返回undefinde

        setInterval(fn(),2000);  // 错误的写法
        setInterval(fn, 2000);   // 正确的写法
        setInterval("fn()",2000);// 正确的写法 了解

    </script>
</body>
</html>
```


二、应用

    常用：轮播图、倒计时
    使用定时器前先学习日期对象

    日期对象


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
        var now = new Date(); // new新创建当前日期对象
        //console.log(now); // 包含日期、时间、时区等信息

        // 获取年月日
        var year = now.getFullYear();
        var month = now.getMonth();
        // alert(month); 
        // 注意：因为西方国家定义0-11为12个月份，0表示一月，要想符合中文习惯就加1
        var day = now.getDate();

        //获取时分秒
        var hour = now.getHours();
        var minutes = now.getMinutes();
        var second = now.getSeconds();
        alert(hour+":"+minutes+":"+second);
    </script>
</body>
</html>
```


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
        var now = new Date(); // new新创建当前日期对象
        //console.log(now); // 包含日期、时间、时区等信息

        // 获取星期几
        // alert(now.getDay);  0-6 0代表周日 通过定义数组weekArr转换成符合中文习惯的星期几

        // 将now放进去，后面d就是now
        var text = dateToString(now);
        alert(text);
        // 定义一个函数将日期格式转换成字符串
        // 先传入一个日期对象d
        function dateToString(d) {
            // 定义个数组，获取星期几，第一个下标0写星期日，跟上面0-6，0代表星期日对应
            var weekArr = ["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];
            // 获取年月日
            var year = d.getFullYear();
            var month = d.getMonth()+1;
            // alert(month); 
            // 注意：因为西方国家定义0-11为12个月份，0表示一月，要想符合中文习惯就加1
            var day = d.getDate();

            //获取时分秒
            var hour = d.getHours();
            var minutes = d.getMinutes();
            var second = d.getSeconds();

            // 注意回车换行拼接字符串需要加个空字符串
            var str = year + "年" + month + "月" + day + "日" + " ";
            str += hour + ":" + minutes + ":" + second;
            str += " " + weekArr[d.getDay()];
            return str;     
        }
    </script>
</body>
</html>

```

    动态时间获取


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 定义一个p元素用来在页面上放时间 -->
    <p id="content"></p>
    <script>
        var p = document.getElementById("content");
        // 先获取当前时间----默认值
        var now = new Date();
        // 调用函数写入p元素
        p.innerHTML = dateToString(now);

        // 开启定时器每隔一秒更新一次
        setInterval(function() {
            // 前面是刚进去进去页面获取一个默认时间，这里是开启定时器时，再次更新获取当前时间
            now = new Date();
            // 再次重新更新写入数据
            p.innerHTML = dateToString(now);
        },1000)

        function dateToString(d) {
            // 定义个数组，获取星期几，第一个下标0写星期日，跟上面0-6，0代表星期日对应
            var weekArr = ["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];
            // 获取年月日
            var year = d.getFullYear();
            var month = d.getMonth()+1;
            // alert(month); 
            // 注意：因为西方国家定义0-11为12个月份，0表示一月，要想符合中文习惯就加1
            var day = d.getDate();

            //获取时分秒
            var hour = twoTwo(d.getHours());
            var minutes = twoTwo(d.getMinutes());
            var second = twoTwo(d.getSeconds());

            // 注意回车换行拼接字符串需要加个空字符串
            var str = year + "年" + month + "月" + day + "日" + " ";
            str += hour + ":" + minutes + ":" + second;
            str += " " + weekArr[d.getDay()];
            return str;     
        }

        // 定义一个函数，当时间：（秒）为个位数时就前面加个0，大于等于10就不加
        function twoTwo(num) {
            // 注意需要返回return 
            return num<10?"0"+num:num;
        }
    </script>
</body>
</html>
```


    倒计时效果（实际就是时间差）
    先取到目标时间、当前时间然后得到时间差，然后进行转换为时分秒等
    例如：距离五月一号多少天多少时多少分多少秒，一般不考虑月份，因为月份比较复杂


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 定义标签放时间 -->
    <div>
        <span>0</span>天<span>0</span>时<span>0</span>分<span>0</span>秒
    </div>
    <script>
        // 找到所有span元素进行后面赋值
        var spans = document.getElementsByTagName("span");

        // 距离端午节多少天多少时多少分多少秒
        // new一个对象获取目标时间,下面定义的时分秒默认0:0:0，可以不写
        var end = new Date("2020-5-1 0:0:0");
        // 获取当前时间
        var now = new Date();

        // 开启定时器每隔一秒计算一次
        setInterval(function() {
            var now = new Date();  // 默认值
            ss = diff(now,end); //调用函数计算时间差
            // document.write(ss + "<br>");
            // 转换为剩余的天、时分秒
            var _d = parseInt(ss/(24*3600));
            var _h = parseInt(ss%(24*3600)/3600);
            var _m = parseInt((ss%3600)/60);
            var _s = parseInt(ss%60);

            // 将上面转化的值赋值
            spans[0].innerHTML = twoTwo(_d);
            spans[1].innerHTML = twoTwo(_h);
            spans[2].innerHTML = twoTwo(_m);
            spans[3].innerHTML = twoTwo(_s);

        },1000);

        // 定义一个函数，获取时间差的毫秒数，然后除以1000获取秒数
        function diff(start,end) {
            // getTime() 是获取从1970-1-1到当前时间的毫秒数
            return (end.getTime() - start.getTime())/1000;
        }

        // 防止秒数出现一位数，导致样式变化定义一个函数
        function twoTwo(num) {
            // 注意：一定要添加return
            return num<10?"0"+num:num;
        }
    </script>
</body>
</html>
```


    设置日期效果(setDate()设置某个月的某天，setMonth()设置某一个月，setYear()设置某年)
    例如：会员到某天过期


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
        var d = new Date();
        // 设置日期:比如设置当期日期后十天过期
        // 如果当前是28号加上10，不会变成38号，系统会自动转换到下一个月
        d.setDate(d.getDate()+10);
        alert(d);
    </script>
</body>
</html>
```


应用

    数码时钟（使用定时器每隔一秒更新时间，然后获取当前时间，最后替换图片路径）


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
    <div id="div">
        <img src="images/0shuma.png" alt="">
        <img src="images/1shuma.png" alt="">时
        <img src="images/2shuma.png" alt="">
        <img src="images/3shuma.png" alt="">分
        <img src="images/4shuma.png" alt="">
        <img src="images/5shuma.png" alt="">秒
    </div>
    <script>
        var imgs = document.getElementsByTagName("img");
        function getTime() {
            var d = new Date();
            var h = d.getHours();
            var m = d.getMinutes();
            var s = d.getSeconds();
            var arr = [parseInt(h/10),h%10,parseInt(m/10),m%10,parseInt(s/10),s%10];
            
            for(var i=0; i<arr.length; i++) {
                imgs[i].src = "images/"+arr[i]+"shuma.png";
            }
        }
        
        // 在定时器没有工作之前，先调用一次函数，防止默认展示的图片展示1秒后才获取到当前时间
        getTime();
        // 开启定时器，保证每秒更新一次可以获取到不同的图片路径
        setInterval(getTime, 1000);
    </script>
</body>
</html>
```

轮播图

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<img src="img/6.jpg" alt="">
	<script>
		var imgs = document.getElementsByTagName("img")[0];
		var imgArr = ["6.jpg","7.jpg","8.jpg","9(1).jpg"]
		var index = 0;
		setInterval(function() {
			// 如果不是顺序播放使用Math.random
			index++;
			// 临界值的判断
			if(index == imgArr.length) {
				index = 0;
			}
			
			imgs.src = "img/"+imgArr[index];
		}, 1000);

	</script>
</body>
</html>
```

勾股定理

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
    <input type="text" id="num1">+
    <input type="text" id="num2">=
    <input type="text" id="num3">
    <script>
        // Math.sqrt(a*a + b*b) a的平方+b的平方
        // 封装一个函数找元素
        function $(id) {
            return document.getElementById(id);
        }

        // 键盘弹起事件
        $("num1").onkeyup = function() {
            // 获取input输入框的值用value，获文本的值用innerHTML
            var v1 = $("num1").value;
            var v2 = $("num2").value;

            // 非空判断
            if(v1=="" ||  v2=="") {
                $("num3").value = "必须是两个数字";
                // return;  注意添加返回
                return;
            }
            if(isNaN(v1) || isNaN(v2)) {
                $("num3").value = "必须两个都是数字";
                return;
            }
            $("num3").value = Math.sqrt(Math.pow(v1,2) + Math.pow(v2,2));
        }

        $("num2").onkeyup = function() {
            // 输入框2，键盘弹起时执行输入框1的事件处理函数
            $("num1").onkeyup();   // 这是方法后面加括号，上面的是属性
        }
    </script>
</body>
</html>
```

