练习：取一个三位数的“个、十、百位”

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
	<script type="text/javascript">
	    var num = prompt("请输入一个三位数的值：");
	    //因为prompt接收的是字符串，所以需要转换为数值
	    var num = parseInt(num);
	    var ge,shi,bai;
	    bai = parseInt(num/100);
	    shi = parseInt((num%100)/10);
	    ge = parseInt(num%10);
	    alert("百位数是："+bai + ",十位数是："+shi + ",个位数是："+ge);
	</script>
</body>
</html>
```
一、运算符

    + 数字转换成字符串：先将数字转换成字符串，再和其它字符串进行拼接
    123+"10" 先把123变成"123",然后与"10"拼接成"12310"
      123+"" ----->"123"
      
    - "123"-10得到110   "123a"-10得到NaN，但NaN也是一种number类型  
    
    "3"-"4" 得到-1 字符串  
    
    "12" * 4得到48
    字符串转换成数字
        Number()  parseInt()  parseFloat()
        
```html
	<script type="text/javascript">
		var a = 123;
		var b = "10";
		c = a + b ;
		alert(typeof c);
		document.write("3"-false);//结果为 3，false转为0
		console.log("20"+2-"6"); //"20"+2---->"202"  结果为196
	</script>
```

二、用户输入

    prompt()为一个输入框，用户可以自定义输入内容。
    
```html
    <script type="text/javascript">
 	var num = prompt("请输入三位数");
 	var bai, shi, ge ;
 	
 	bai = parseInt(num/100);
 	shi = parseInt(num/10)%10;
 	ge = num%10;
 	
 	alert("百位数是:"+bai+";十位数是:"+shi+";个位数是:"+ge);
	</script>
```

三、自增自减

    i++与++i比较 无论什么情况最后i都会增加1,区别就是i++参与运算时采用的是i一开始值，++i参与运算采用的是i加1后的值
        i++ 或 i--  是先将i的值赋值给变量，再自增或自减1；
        ++i 或 --i  是先自增或自减1，再赋值给变量；
        
```html
<script type="text/javascript">
	var j = 7;
	var i;
	i = j++;

	alert(i+":"+j);//7:8

	var j = 7;
	var i;
	i = ++j;

	alert(i+":"+j);//8:8
</script>
```

四、关系运算符

    关系运算符组成的关系表达式结果是一个布尔值 true 成立 false不成立
    
```html
<script type="text/javascript">
	console.log(10 > 9);
	console.log(10 < 9);
	console.log(100 >= 74);
	console.log(24 <= 34);
	console.log("10" > "9");//false 字符串数字比较，一个个字符对比，1<9,所以false
	console.log("xikl" < "xili");//true 按字母排序顺序一个个比较，排序靠后的较大
	console.log("67" > 24);//true 纯数字字符串会隐式转换成数字比较
	console.log("23ik">11); //false
	console.log(10 == 10);//true 不严格相等，只要内容相等就相等即"10"==10
	console.log("10" == 10);//true 
	console.log(10 === "10");// false 严格相等，内容和类型都要相等
	console.log(8 != 8); //false  !=是对==的否定
	console.log("5"!=5); // false 
	console.log(10 !== 10); //false !==是对===的否定
	console.log("5"!==5); // true 
</script>
```

五、逻辑运算符

    && || !
    * && 并且 左右两个表达式全是true结果才是true，其他情况全是false
    * || 或 只要有一个表达式为true结果就是true
    * 表达式为true加!后边false
    
```html
<script type="text/javascript">
	console.log(10 > 10 && 37 >18);
	console.log(10 == 10 && 37 >18);
	console.log(10 > 10 || 37 >18);
	console.log(!(10 == 10));
</script>
```

    短路现象
    
    逻辑&&  当第一个表达式为false,整个逻辑表达式结果确定就是false,没有必要（也不会）执行后面的表达式
    || 当第一个表达式为true(非0) 结果就是第一个 表达式的值，此时不会执行第二个表达式
    
```html
<script type="text/javascript">
	var num = 399;
	console.log(50<49 && --num); //false
	console.log(num);  //399

	console.log(50>49 && --num); //398
	console.log(num);  //398
	
	var num1 = 199;
	console.log(1 || num1++); //1
	console.log(num1);  //199

	console.log(0 || num1++);  //199 
	console.log(num1);  //200
</script>
```

六、条件运算符

    表达式1?表2:表3  先执行表1，表1成立返回表2作为最终结果 否则返回表3(三目运算)
   
```html
<script type="text/javascript">
	console.log(199>200?"正确的":"错误的");
</script>
```

七、赋值运算符

```html
	<script type="text/javascript">
	    // = 赋值运算符 不是等于
	    var num = 10;
	    var num2 = 12 + 6;
	    // += -= *= /= %=  复合运算符
	    num += 1;// num = num + 1; num++; ++num
	    console.log(num);
	</script>
```

八、类型转换

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
<script type="text/javascript">
	//parseInt parseFloat Number Boolean toString

	//parseInt转换为number类型,遇到小数点或者非数字字符就停止
	console.log(typeof parseInt("1234"));  //number 1234
	console.log(parseInt("12.56"));        //12
	console.log(parseInt("-2344.33"));     //-2344
	console.log(parseInt("23.33kin"));     //23
	console.log(parseInt("44kk.e33"));     //44
	console.log(parseInt("kin335"));       //NaN
	console.log(parseInt( ));              //NaN

	//parseFloat转换为number类型的浮点数
	console.log(parseFloat("123.55"));     //123.55
	console.log(parseFloat("384kk.55"));   //384
	console.log(parseFloat("kk33.1"));     //NaN
	console.log(parseFloat("45.2k3"));     //45.2

	//Number 将其它类型转换为Number类型
	//Number必须要求字符串是纯数字的字符串，假如含有其他非数字或非小数点的字符则统一结果是NaN
	console.log(Number(true));             //1
	console.log(Number(false));            //0
	console.log(Number("23.566"));         //23.566
	console.log(Number("sss3455"));        //NaN

	//Boolean 把其它类型转换为布尔类型
	console.log(Boolean(""));              //false
	console.log(Boolean(0));               //false
	console.log(Boolean("123"));           //true
	console.log(Boolean(123));             //true

	//toString 转换为字符串
	var n=38;
	n = n.toString();
	alert(n);
	//也可直接拼接成字符串
	n = ""+38

</script>
</body>
</html>
```

    * 以某种进制输出 toString()

```html
<script type="text/javascript">
	var num = 42;
	var get_num = num.toString(2);
	alert(get_num);
</script>
```