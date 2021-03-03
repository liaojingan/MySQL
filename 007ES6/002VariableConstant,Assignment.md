### 变量

     声明变量
    var a = 100
    let b = 'hello'
    
### let的三大特性（为什么要使用let）

     特征一：不存在变量提升，必须要先声明，再使用
       console.log(a); // 报错ReferenceError
       let a = 2;
       
```js
# 变量声明提升
console.log(a);
var a = 100;
console.log(a);
# undefined
# 100

# let不可变量提升，否则报错
console.log(a);
let a = 100;
console.log(a);
```
       
     特征二：不能重复声明
       let b = 100
       let b = 'hello' // 报错 SyntaxError
       
```js
let a = 100;
console.log(a);

let a = 200;
console.log(a);

# let变量不可重复声明
```
       
     特征三：块级作用域，变量只在代码块内有效
       function func() {
            let n = 5;  # 这个n在大的func函数中有效
            if (true) {
                let n = 10; # 这个n只在if中有效
            }
        console.log(n); // n = ？ 5 如果使用var则n=10；则存在值的污染
        }
        
### 常量（作用：增强代码可阅读性）

    * 一旦声明，常量的值就不能改变
    
     声明常量
        const PAGE_SIZE = 100
        const PI = 3.1415926
        
### const的三大特征

     特征一：声明必须赋值(必须初始化)
        const NAME; // 报错 SyntaxError
        NAME = 100
        
     特征二：常量是只读的，不能重新赋值
        const PI = 3.1415926
        PI = 3.141592654 // 报错 TypeError
        
     特征三：块级作用域，只在代码块内有效
    
        if (true) {
            const PI = 3.1415926
        }
        console.log(PI) // 报错 ReferenceError
        
    应用场景：比如订单的状态（待支付）跟服务器端是约定好的，然后用常量定义界面就显示去支付的按钮
    然后再标记请求来源、小程序、app或H5
    
### 解构赋值

    按照一定的结构提取出来，赋值给新的变量
     场景一：数组的解构赋值
     场景二：对象的解构赋值
     场景三：字符串的解构赋值
    
    python中的结构，比如将a=(1,2)中的1赋值给c、2赋值给d
    
```python
a = (1, 2)
c, d = a 
```

### 数组的解构赋值
    
    * 按顺序将值赋值给对应的变量
    
    let a = [2, 4, 5];
    let [a1, a2, a3] = a;

    console.log(a1);
    console.log(a2);
    console.log(a3);
    
    * …表示解构运算符，将剩余的内容赋值
    
```js
let a = [2, 4, 5]
let [b1, ...b2] = a;

console.log(b1);
console.log(b2);

2
[ 4, 5 ]
```

    * 解构赋值失败，变量值为undefined
 
```js
let [e, f] = [1];
console.log(e)
console.log(f)

undefined
```

    * 防止解构失败，给变量默认值
    
```js
let [g, h=100] = [1];
console.log(g)
console.log(h)
```   

### 对象的解构赋值

    * 按顺序将值赋值给对应的变量  注意结构
    
```js
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
console.log(foo)
console.log(bar)
```

    * 可以解构对象中的常量、方法
 
```JS
console.log(Math.PI) # 直接运行得到PI值3.1415926
let { PI, sin } = Math  # Math是一个对象，可以传入多个值PI,sin
console.log(PI)
console.log(sin(PI/2)) // sin(90°)
```

    * 解构赋值失败，则为undefined，可设置默认值
    
```js
let {x, y = 5} = {x: 1}
console.log(x)
console.log(y)
```

    * 重新指定变量名称
    
```js
let { color: sky } = {color: 'blue’}
console.log(sky
```

    * 复杂对象的解构赋值
    
```js
let {title, author: {name, age}} = {
    title: '新闻标题',
    author: {
        name: '张三',
        age: 23
    } 
}
console.log(name)
console.log(age)
```

    对象解构赋值的应用：通过Ajax库异步请求的时候，比如登录需要传入用户名密码，最终需要
    得到一个回调，返回200则成功
    
```js
$.post(url, data, function({code, objects}) {
if (code === 200) {
// 请求成功，执行正确的业务逻辑代码
}
})
```

### 字符串的解构赋值

    * 字符串可以看做是“伪数组”（注：它不是真的数组）
    
```js
const [a, b, c, d, e] = 'hello'
console.log(a)
console.log(b)
let {length} = 'hello'
console.log(length)
```

### 函数、箭头函数 设置默认值

    ES6之前的函数如何指定默认值
    
    function point(x, y) {
        x = x || 0;
        y = y || 0;
    }
    
    ES6之后
    
    function point(x = 0, y = 0) {
        console.log(x)
        console.log(y)
    }
    
    * 未设置默认值且不传对应参数时，值为undefined
    
    function point(x, y = 0) {
        console.log(x)； // undefined
        console.log(y)； 
    }

    * 带默认值的参数顺序，提示：将带默认值的参数放于最后
    
    function point(x = 0, y, z) {
        console.log(x)；
        console.log(y)；
        console.log(z)； 
    }  
    point(1, 3)
    # 得出x=1, y=3, z=undefined
    
    * 注意：参数变量(形参)不可重复声明
    
    function point(x = 0, y = 0) {
        let x = 0；
        const y = 1； # 不可重复
    }
    
    * 当形参为对象时，可使用解构赋值
    
    function fetch(url, { body = '', method = 'GET', 
    headers = {} }) {
    $.ajax({
        url,
        method
    })
    }
    
### 对象中的函数简写

    改进前：
    let UserA = {
        name: '张三',
        age: 23,
        info: function( ) {
            return this.name + this.age
        } 
    }
    
    改进后：
    let UserB = {
        name: '张三',
        age: 23,
        info() {
            return this.name + this.age
        } 
    }
    
### 箭头函数

     定义箭头函数
        let f1 = v => v;
        
        // 等同于
        let f1 = function (v) {
            return v;
        }
        
        let f2 = (a, b) => a + b;
        
        // 等同于
        let f2 = function (a, b) {
            return a + b;
        };
        
     函数体包含多条语句，使用{}包含语句块
    
       let f3 = (a, b) => {
            console.log(a, b)；
            return a + b； 
       }
       
     箭头函数的使用场景——数组遍历
    
       let arr1 = [1,2,3]
            arr1.map(function (x) {
            return x * x;
       });
       
       let arr2 = [1,2,3]
       arr2.map(x => x * x);
       
     注意：箭头函数体内的this指向定义时所在的对象，而非实例化后的对象（在函数定义时绑定），类似于Python中的self
    
       let UserC = {
            name: '张三',
            age: 23,
            info: () => {
                return this.name + this.age
            } 
       }
       console.log(UserC.info
       
### 理解this

     指函数执行过程中，自动生成的一个内部对象，是指当前的对象，只在当前函数内部使用
         运行时跟运行环境绑定
            浏览器: this === window
            Node 环境：this === global
         当函数被作为某个对象的方法调用时，this指向那个对象
        
     再次理解箭头函数中的this(指向定义时所在的对象)
    
    let MyObj = {  # 声明MyObj对象
        a() {  #  a()不使用箭头函数，打印时指向MyObj
            console.log('a', this) // MyObj
            setTimeout(()=> {
                console.log('timeout', this) // MyObj
            }, 100)
        },
        b: () => {  # 箭头函数b: ()指向全局对象window，b不能访问a()或者其他变量
            console.log('b', this) // window
        } 
    }