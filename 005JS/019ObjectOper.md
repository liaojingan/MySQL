基本数据类型

    Number String Boolean null undefined

引用数据类型

    Object Array Date Function 正则表达式
    函数和数组都是对象

对象(属性:属性值)

    由无序的属性集合组成{k:v,k:v,k:v}
    属性值不仅有信息还有行为，行为对于程序来说就是方法或者函数    

    对象直接量
    var list = {
        "name":"lisi",
        "age":22,
        "sex":"男"
    }

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
        // 描述一个用户信息，用定义参数值和对象的方式存储对比
        var name = "lisi";
        var age = "29";
        var sex = "男";

        // 用对象描述张三，对象是一个整体
        var zs = {
            name: "zhangsan", // 属性  属性名：属性值
            age: "20",
            sex: "女",
            // 行为（函数或者方法）
            study: function() {
                alert("great!");
            },
            eat: function() {
                alert("吃货");
            }
        }
    </script>
</body>
</html>
```


    对象的成员访问：对象.成员
    动态添加属性以及行为

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
        // 描述一个用户信息，用定义参数值和对象的方式存储对比
        var name = "lisi";
        var age = "29";
        var sex = "男";

        // 用对象描述张三，对象是一个整体
        var zs = {
            name: "zhangsan", // 属性  属性名：属性值
            age: "20",
            sex: "女",
            // 行为（函数或者方法）
            study: function() {
                alert("great!");
            },
            eat: function() {
                alert("吃货");
            }
        }

        // 对象成员的访问：对象.成员
        console.log(zs.name);
        console.log(zs.sex);
        // 注意调用对象的方法加括号，还有不可以单独写成study(),不然会默认全局查找window.study()
        console.log(zs.study());

        // 因为随着时间推移，信息可能有所补充，所以就会出现动态添加属性
        zs.issingel = false;
        alert(zs.issingel);

        // 动态添加行为
        zs.coding = function() {
            alert("动态添加行为");
        }
        zs.coding();
    </script>
</body>
</html>
```

JS基本类型和对象类型（JS中可以一切看做对象）

    基本类型不支持添加属性

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
        // 基本类型不能动态添加属性
        var num = 10;
        num.index = 111;
        alert(num.index);  // undefined
    </script>
</body>
</html>
```

值的赋值和对象赋值不同之处

    对象赋值指的是地址的赋值：比如一个人先去图书馆借书，然后撕了一张纸，后面
    一个同学也去借同一本书，那这本书也是被撕了的，是同一本书；
    相比对象赋值也是，修改的也是同一个地址

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
        // 值的赋值
        var i = 10;
        var j = i;
        i = 19;
        alert(i);  //10

        // 对象的赋值
        // 对象存储的值在堆内存里，占用了一块空间，内存有个地址，对象的赋值obj={name:"zs"}
        // 是说把这个地址赋值了，所以obj存储的是对象的地址，然后obj赋值给obj1,这样两个都指
        // 向同一个对象，所以修改对象为obj1.name = "lisi"，修改的同一个地址，所以obj和obj1都为lisi  
        var obj = {name:"zs"};
        var obj1 = obj;
        obj1.name = "lisi";
        alert(obj.name);  //lisi

        var arr = [3,5,6];
        var brr = arr;
        arr[0] = 8;
        alert(brr); // arr和brr都是[8,5,6]

    </script>
</body>
</html>
```

数据交换格式json：标准的数据交换格式

    前端和后端进行数据通信，后台会传给前端数据，前端获取展示，所以数据需要遵循一定的格式
    主流格式json，以前xml

    json格式和普通对象格式对比
    json数据格式，属性**必须用双引号**引起来  {"name":"lisi"}
    普通对象格式，属性可以使用双引号引起来，也可以不用 {name:"lisi"}

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
	   // json 一种标准的数据交换格式 属性必须用双引号引起来
	   var lisi = {
           "stuName": "lisi", // 属性 属性名:属性值
           "stuAge": 20,
           "stuHeight": "178cm",
           "stuTel": "18866666666",
           // 行为 
           "study": function() {
           		alert("good good study day day up");
           },
           "eat": function() {
           	    alert("吃货一枚!!!");
           }
       };

       // json数据访问跟对象访问属性一致
       alert(lisi.stuAge);
       // 调用方法也是一致的，不用跟上面一样再加个alert
       lisi.study()
	</script>
</body>
</html>
```


for in 循环

    对对象或者json都起作用


```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
    </head>
    <body>
        <script type="text/javascript">
        // json 一种标准的数据交换格式 属性必须用双引号引起来
        var lisi = {
            "stuName": "lisi", // 属性 属性名:属性值
            "stuAge": 20,
            "stuHeight": "178cm",
            "stuTel": "18866666666",
            // 行为 
            "study": function() {
                    alert("good good study day day up");
            },
            "eat": function() {
                    alert("吃货一枚!!!");
            }
        };

        // json数据访问属性的两种方式
        // 第一种：跟对象访问属性一致；第二种：对象["属性名"]，注意属性名加双引号，否则表示变量
        alert(lisi.stuAge);
        alert(lisi["stuHeight"]);
        // 调用方法也是一致的，不用跟上面一样再加个alert
        lisi.study();


        /*
           对象["属性名"] === 对象.属性名
           对象[变量] 不能这样如对象.变量 假如这样写表示对象的有个属性名是这个变量名
       */
        for(var k in lisi) {
            // k代表每一个属性(属性名:属性值)
            // lisi[k] 代表属性k对应的属性值
            console.log(k + ":" + lisi[k]);
        }
        </script>
    </body>
    </html>
```


对象获取

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
        // 打印所有的路径和文字描述即打印所有数据
        var json = {
            "url":["1.jpg","2.jpg","3.jpg","4.jpg","5.jpg"],
            "desc":["图片一","图片二","图片三","图片四","图片五"]
        }

        
        for (var k in json) {
            // json[k]代表json数据中的某一个属性的值
            // json[k][i]中的[i]表示下标
            for (var i=0; i<json[k].length; i++) {
                console.log(json[k][i]);
            }
        }
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
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <ul></ul>
    <script>
        // 定义一种数据结构，存储四个用户信息
        // 四个用户可以用数组存储，每个用户可以用json格式表示
        var users = [{
            "uname":"user1",
            "pswd":"123"
        },{
            "uname":"user2",
            "pswd":"456"
        },{
            "uname":"user3",
            "pswd":"789"
        },{
            "uname":"user4",
            "pswd":"101"
        }];

        // 把用户显示在ul列表中
        var getUl = document.querySelector("ul");
        for (var i=0; i<users.length; i++) {
            var createLi = document.createElement("li");
            // users[0] 下标为0的数据，users[i].name下标为0里面uname的值
            createLi.innerHTML = "用户名" + users[i].uname + "密码是" + users[i].pswd;
            getUl.appendChild(createLi);
        }
    </script>
</body>
</html>
```

        计算器练习省略

总结

    js关于dom操作
      找元素
            document.querySelector()
            document.querySelectorAll() 
            document.getElementById()    浏览器都兼容，但只能在document中使用
            document.getElementByTagName() 注意返回的是列表，需要加上[]
            document.getElementsByClassName() ie9+可以使用
            document.getElementsByName()  ie中只对表单元素name中
            
            6个方法
            document.documentElement  获取html
            document.body 获取body
            document.head 获取head
    属性    childNodes/children /firstChild/lastChild/nextSibling/previousSibling 


client、offset、scroll三大家族（常用于特效）

       width/height/left/top
       offsetParent

    (1)clientWidth = width + 左右padding
       clientHeight = height + 上下padding
       clientWidth 为可视区域的宽度   width + 左右pdding与内容是否溢出无关

       主要应用于：当点击页面按钮弹出一个框需要水平居中、垂直居中
       先得到整个屏幕的可视区域宽度，减去自己盒子的宽度然后除以2 

       clientTop 上边框的宽度  clientLeft 左边框的宽度  没有clientRight

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
    .box {
        width: 200px;
        height: 210px;
        padding: 15px;
        border: 10px  solid skyblue;
        margin: 50px;
    }
    </style>
<body>
    <div class="box" id="box">
        案发时放点方式的噶的噶多少个但是还是申购赎回
        案发时放点方式的噶的噶多少个但是还是申购赎回
        案发时放点方式的噶的噶多少个但是还是申购赎回
        案发时放点方式的噶的噶多少个但是还是申购赎回
        案发时放点方式的噶的噶多少个但是还是申购赎回
        案发时放点方式的噶的噶多少个但是还是申购赎回
        案发时放点方式的噶的噶多少个但是还是申购赎回
    </div>
    <script>
        
    </script>
</body>
</html>
```

![clientWidth](../picture/clientWidth.png)
![clientHeight](../picture/clientHeight.png)


    offsetWidth 左右border+左右padding+width
    ......Height .... 上下border+上下padding+height

![offsetHeight](../picture/offsetWidth.png)

    这两个值是有误差的
    scrollWidth  左padding+内容真实的宽度（包含溢出内容）
    ......Height 上padding+内容真实的高度（包含溢出内容）

