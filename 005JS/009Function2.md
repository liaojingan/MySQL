函数递归

    函数递归------自己调用自己,并且需要定义边界极限
    求1+2+3+4+...+n n传入
    
```html
<script type="text/javascript">
    function getSum(n) {
    	if(n===1) {
    		return 1;
    	}
    	return n+getSum(n-1);
    }

    var sum = getSum(8);
    console.log(sum);
</script>
```

```html
<script type="text/javascript">
   // 求1+3+5+7+...n
   function getSum2(n) {
   		if(n === 1) {
   			return 1;
   		}
   		return n+getSum2(n-2);
   }
   //规定n只输入奇数
   alert(getSum2(11));
</script>
```

```html
<script type="text/javascript">
   // 斐波那契数列 1 1 2 3 5 8...  打印前15项之和
   function getSum3(n) {
   		if(n > 1) {
   			var sum = getSum3(n-1)+getSum3(n-2);
   			return sum;
   		}
   		return 1;
   }

   console.log(getSum3(15));
</script>
```

函数的作用域

    全局变量 
           1 在函数外部定义的变量
           2 在任何地方可以使用  
           3 不加var默认是隐形的全局变量,无论在什么位置定义都是全局 
           
         局部变量
            1 函数体内部通过var定义的变量
            2 局部变量只能在所在函数内使用
            3 当局部变量与全局变量同名时,用自己的 
            
```html
<script type="text/javascript">
   function fn() {
           var num = 15;
           console.log(++num); // 16
       }  
       var num = 10;
       
       fn();
       console.log(num); //10
</script>
```

```html
<script type="text/javascript">
   var a = 100;
       function fn() {
           b = 10; //此处这个b是隐形的全局变量
       }
       fn();
       console.log(b);  //10
</script>
```
变量声明提升

    变量初始化不提升    var x=3;
    声明的变量会提升    var x;

```html
<script type="text/javascript">
	//下面的代码等价于 var b; console.log(b); b = 12;
   console.log(b);// undefined 不是错
       var b = 12;
</script>
```

    浏览器
          js解析器或js引擎解析js代码
          1 预解析 没有解读代码之前的操作 
            会找var function 进行变量声明提升(注意只是定义提升)
          2 逐行去解读代码   
          
函数首先会被提升，然后才是变量提升
    
    函数提升优先级比变量提升要高，且不会被变量声明覆盖，但是会被变量赋值覆盖。
```html
alert(a); //结果为函数
	var a=8;
	function a() {
		console.log("dsjkl");
	}

	alert(a); //8
```

```html
<script type="text/javascript">
	console.log(foo);
	function foo(){
	    console.log("函数声明");
	}
	var foo = "变量";	
</script>
```
    上面的代码就相当于
    
```html
function foo(){
		console.log("函数声明");
	}
	var foo;
	console.log(foo);
	foo = "变量";
```

