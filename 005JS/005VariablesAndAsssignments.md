1、变量

    *"未知数"本质上相当于一个容器，可以放任何数据
    
2、语法

    一、变量定义以及变量赋值
    二、格式： var 变量名
        变量名命名规则：组成部分: _ $ 字母 数字
	      第一个字符不能为数字 
	      区分大小写 比如 a 和 A 是不同的变量名
	      不能是js的关键字和保留字
	      
	   var a;
	   var _;
	   var $;
	   var o0_00;
	   var a123;
	   var var;// 错误
	   var ~=aa;  
	             
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
		//变量定义
		var a;
		//给变量赋值
		a = 666;
		console.log(a);//666
	</script>
</body>
</html>
```

3、赋值方式
        *先定义后赋值
        *定义的同时赋值
        
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
		var a1;
	    a1 = 123.56;// 把123.56赋值给左边变量a1
	  
	    // 定义同时赋值
	  
	    var a1 = "alongQQ382867197";
	    alert(a1);
	    
	    var a = 10, b = 20, c = 30;
	    console.log(a+b+c);
	    var d;
	    console.log(d); // 不是错误 而是undefined 表示变量定义 但没有赋值
	    console.log(e); // e is not defined 报错 表示变量没定义就使用 语法报错
	</script>
</body>
</html>
```
![变量赋值](../picture/JS02.png)

4、变量声明提升

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
		//结果为undefined
		console.log(a);
		var a = 10;
		console.log(a);
//等价
		//浏览器js引擎会把变量a的定义提升到所有语句之前
		var a;
		console.log(a); //变量定义了，没有赋值，结果为undefined
		a = 10;
		console.log(a);

	</script>
</body>
</html>
```
    