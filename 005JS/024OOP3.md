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
        // 定义一个构造函数（类）
        function People() {
            this.name = "lisi",
            this.age = 23
        }
        
        // new一个对象，赋值给res，这个res就叫（实例对象）
        var res = new People();
        // 打印实例
        console.log(res);
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
    <script>
        function A() {
            this.m = 10;
        }

        function B() {
            this.m = 20;
        }

        // 相当于调用A函数并把this指向改为B即B.m = 10
        // (函数.m)可以用这种格式原因：函数也是一种对象，所以可以添加属性
        A.call(B); 
        // 同理调用B且改变指向所以A.m = 20
        B.call(A);

        // new一个对象四部曲：{},然后this指向这个对象，所以{m:10}，执行后返回到A
        var a = new A(); 
        // {m:20}
        var b = new B(); 
        console.log(a.m == B.m); // true
        console.log(b.m == A.m); // true
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
    <script>
        function getLength() {
            // 普通函数的this看上下文，构造函数的this是空对象{}
            return this.length;
        }

        function foo() {
            // 函数名直接调用，所以这个this是window
            this.length = 1;
            return (function() {
                var length = 2;
                return {
                    length: function(a,b,c) {
                        return this.arr.length;
                    },
                    arr : [1,2,3,4],
                    info : function() {
                        return getLength.call(this.length);
                    }
                }
            })();
        }

        var x = foo().info();
        alert(x); // 3
    </script>
</body>
</html>
```


构造函数操作DOM

    使用构造函数动态添加图片的优势：可以new多个对象快速添加图片

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
        function CreateImage(url) {
            // 创建一个img元素用属性dom记住
            this.dom = document.createElement("img");
            // 那这个dom就是img元素了可以设置src路径
            this.dom.src = url;
            // 把上面的过程叫上树（上DOM树）
            document.body.appendChild(this.dom);
        }

        // new一个对象
        var obj = new CreateImage("images/1.jpeg"); // {dom:img元素}
        console.log(obj);
    </script>
</body>
</html>
```


    用下面的方式:对象直接添加方法是不好的，如果有几十个人，那就需要new几十个对象，每个对象有几个方法，
    而且每个对象的方法逻辑都相似，这样就会造成代码冗余


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
        function People(name,age,sex) {
            // 添加属性
            this.name = name,
            this.age = age,
            this.sex = sex,
            // 添加方法
            this.sayHi = function() {
                alert("你好,我是" + this.name + ",年龄是" + this.age);
            }
        }

        // 返回一个对象Sirwang
        var Sirwang = new People("王某某",48,"男");
        // 对象调用类里面的函数
        Sirwang.sayHi();
        console.log(Sirwang);

        var zhenzhen = new People("珍珍",20,"女");
        zhenzhen.sayHi();

        // 创建第一个Sirwang对象时是自己的属性值是function，而zhenzhen这个是另一个对象
        // 只是说这两个不同的对象逻辑相似
        console.log(Sirwang.sayHi == zhenzhen.sayHi) // false

    </script>
</body>
</html>
```

原型链上添加方法

    对比上面的方法优点：
    方法只需要写一遍，之后这个构造函数的实例，创建出来的对象就自动拥有了这个方法

    对象打点调用方法（wzz.sayHi()）有个机制，调用的时候会先在对象自身查找，如果没有
    就会到原型链上去查找方法，有就调用

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
        /*
          每一个构造函数都有一个属性prototype属性,该属性指向了一个空对象
          可以用console.dir(People)打印出来查看
          构造函数的prototype的类型是对象object，所以可以打点添加属性
        */
        function People(name,age,sex) {
            // 添加属性
            this.name = name;
            this.age = age;
            this.sex = sex;
        }

        // 把sayHi()函数绑定到prototype属性中
        People.prototype.sayHi = function() {
            alert("你好,我是" + this.name + ",年龄是" + this.age);
        }

        // 把方法加在原型上，实例都是调用的原型上这个方法
        // 所以现在这个值是true console.log(wzz.sayHi == zs.sayHi) // true
        var wzz = new People("王珍珍",21,"女");
        var zs = new People("张三",21,"男");
        console.log(wzz);
        console.dir(People);

        console.log(People.prototype === wzz.__proto__ && wzz.__proto__=== zs.__proto__);

        /*        prototype:原型
          People———————————————>People.prototype
            |                      sayHi() 
            | new                    
            |                        ^ 
           ldh ----------------------| 
        实例都有这个属性__proto__ 最终也是指向原型 
        */
        // People.prototype 叫做构造函数的原型
        // wzz zs 原型的对象
    </script>
</body>
</html>
```

