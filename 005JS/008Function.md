```html
<script type="text/javascript">
    //方案一
	// 素数-质数  只能被1和自己整除的数
	// 判断一个数是否为素数
	var num = parseInt(prompt("请输入数值："));
	var bool = true;
	for(var i=2; i<num; i++) {
		if(num%i == 0) {
			bool = false;
			break;
		}
	}

	if(bool) {
		console.log(num+"：是素数");
	} else {
		console.log(num+"：不是素数");
	}
</script>
```

```html
<script type="text/javascript">
	//方案二
	var count = 0;
	var num = parseInt(prompt("请输入数值："));
	for(var i=1; i<=num; i++) {
		if(num%i === 0) {
			count++;
		}
	}

	if(count === 2) {
		console.log(num+"：是素数");
	} else {
		console.log(num+"：不是素数");
	}
</script>
```

函数

```html
<script type="text/javascript">
	var count = 0;
	function primer(num) {
		for(var i=1; i<=num; i++) {
			if(num%i === 0) {
				count++;
			}
		}
		if(count===2) {
			console.log(num+"是一个素数");
		} else {
			console.log(num+"不是一个素数");
		}
	}
	primer(100);
</script>
```

函数的具体语法

```html
// 定义函数
	    /*  定义方式一 
            function 函数名() {
	            // 函数体------功能具体实现
            }
	    */
	function printLines() {
		console.log("---------------");
	}
	//函数调用方式：函数名()
	printLines();


// 定义方式二  函数表达式(注意 必须先定义后调用)

	var printMessage = function() {
		console.log("先定义后调用");
	}
	printMessage();
</script>
```

函数参数

```html
<script type="text/javascript">
	// 定义一个函数 求两个数的和
	// 定义时候a b我们称为形式参数 将来函数调用时 由实参传递到形参
	function printSum(a,b) {
		var sum = 0;
		sum = a + b;
		console.log(sum);
	}

	printSum(10,29); //调用
</script>
```

arguments用法

    arguments.length-----表示函数调用实参个数
    函数名.length 指的是函数形参个数

```html
<script type="text/javascript">
	function getSum(a,b) {
		console.log(arguments.length);//打印形参个数
		console.log(getSum.length); //函数名.length 打印实参个数
		if(arguments.length === getSum.length) {
			alert(arguments[0]+arguments[1])
		} else {
			alert("形参的个数和实参的个数不相等");
		}
	}

	getSum(20,10,28);

 // 定义一个函数 求任意个数的和  
	     function fnAdd() {
	     	var sum = 0;
	     	for(var i=0; i<arguments.length; i++) {
	     		sum += arguments[i];
	     	}
	     	alert(sum);
	     }

	     fnAdd(1,8,70,45);
	
</script>
```

函数的返回值

```html
	<script type="text/javascript">
	     function getSum(a,b) {
             var sum;
             sum = a + b;
             //alert(sum);
             return sum; // 1 返回一个值 返回到函数调用的地方 2 函数立即结束调用
             console.log("我一辈子也不会轮到我执行");
	     }

	     var result = getSum(3,6); // 用result记住函数返回值
	     document.write(result);
	</script>
```
