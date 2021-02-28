一、数据类型

    1、基本数据类型
        Number   数字类型
        String   字符串
        undefined 
        Boolean 布尔类型
        null
        
    2、复杂数据类型
       Object
     
    注意：变量的数据类型由存储的数据类型决定
       
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
		//typeof检测数据类型
		console.log(typeof 11);//number
		console.log(typeof undefined);//undefined
		console.log(typeof true);//boolean
		console.log(typeof null);//object

		var b="111";
		alert(typeof b);//string 
	</script>
</body>
</html>
```
![数据类型](../picture/JS03.png)

二、数据类型的转换

    数字转换成字符串：先将数字转换成字符串，再和其它字符串进行拼接
      23+"10" 先把23变成"23",然后与"10"拼接成"2310"
      23+"" ----->"23"
      
    字符串转换成数字
        Number()  parseInt()  parseFloat()
        
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
		//数字转换为字符串
		console.log(typeof 23+"10") //"2311"

		//取整
		var num = parseInt(12.999); //12
		alert(num);

		//字符串转换成数字
		console.log(parseInt("-199")); //-199
		console.log(parseInt("199"));  //199
		console.log(parseInt("199.99")); //199
		console.log(parseInt("199jing")); //199
		console.log(parseInt("jing"));  //NaN 无法用数字表达所以为NaN
		console.log(parseInt("中文"));  //NaN
		console.log(parseInt("Infinity"));  //NaN  不是以数字开头
		console.log(parseInt("anan199"));  //NaN

        console.log(parseInt("10"));  //10 没有第二个参数进制时，默认按十进制解析
		console.log(parseInt("10",8));  // 8
	</script>
</body>
</html>
```
        
![数据类型转换](../picture/JS04.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
		console.log(typeof parseFloat("333"));
		console.log(parseFloat("333.3566")); //数字333.3566
		console.log(parseFloat("333.35.55")); //数字333.35
		console.log(parseFloat(".3555")); //数字0.3555
		console.log(parseFloat(".78e3")); //数字780
		console.log(parseFloat(".78e3a")); //数字780
		console.log(parseFloat("a.78e3")); //NaN
		console.log(parseFloat("JFSJ")); //NaN
	</script>
</body>
</html>
```
![数据类型转换](../picture/JS05.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
		// prompt打印出来的是string类型，如果要转成数字则要加入parseInt
		var age = parseInt(prompt("请输入你的年龄",23));
		age = age+1;
		console.log(age); 
	</script>
</body>
</html>
```

    