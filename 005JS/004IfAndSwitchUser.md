1、isNaN()：判断"是,不是数字"，不是数值返回true,否则返回false

    注意：当传入的是纯数字的字符串时，会隐式转换为数字
   
```html
<script type="text/javascript">
	console.log(isNaN("123"));        //false
	console.log(isNaN("df123"));      //true
	console.log(isNaN("12.34"));      //false
</script>
```

2、eval():执行js表达式

```html
<script type="text/javascript">
	eval("alert('结束了')");
	var num = 23
	sum = eval(eval('num+4'));
	alert(sum);
</script>
```

3、等于(==)和严格等于(===)

```html
<script type="text/javascript">
	console.log(null == undefined); //true
	console.log(null === undefined); //false
	// 布尔类型与其它类型相比较，先把true转为1，false转为0,再进行比较
	console.log("javascript" == true); //NaN 与 1 进行比较   false
	console.log("javascript" == false); //NaN 与 0 进行比较  false
	console.log("1" == true); //true
	console.log("0" == false); //true
</script>
```

4、if 分支结构

    js三种控制结构  
        顺序结构
	    条件结构(分支结构)
	    循环结构(重复结构) 
	    
	分支结构
	      if (表达式) {
	         // 语句
	      }else{
	      
	      }
	      
```html
<script type="text/javascript">
	age = parseInt(prompt("请输入你的年龄："));
	if(age>18) {
		alert("你已经成年了,该干嘛干嘛去！");
	} else {
		alert("你还未成年呢，小子！");
	}
</script>    
```

    其他类型转布尔类型
      undefined转成布尔值false
      null  ..... false
      数字----> +0 -0 NaN都会转false 其他为true
      字符串----> "" '' 转false 其他为true
      对象 ------> true 


5、if嵌套结构      
```html
<script type="text/javascript">
	//  加油站  92  <=80L  0.7  >80L  0.65 
	//  95   <=100L 0.72  >100L 0.7
	// 提示用户输入加油的类型
	var type = parseInt(prompt("请输入你需要的类型:"));
	var v = parseInt(prompt("输入你需要添加的体积:"));
	var total = 0;

	if(type==92) {
		// 判断不同体积油量，所需要的价格
		if(v<=80) {
			total = v*0.7;
		} else {
			total = v*0.65;
		}
	} else if(type==95) {
		if(v<=100) {
			total = v*0.72;
		} else {
			total = v*0.7;
		}

	}
	else {
		alert("你输入类型不正确，请再次输入！");
	}
	alert("你需要支付"+total+"元!");
</script>
```

6、switch用法

    拿switch后面的值与大括号里所有的case比较，假如找到对应的case值相等，
    就从该case后面执行语句,直到遇到break或者switch结束，假如没有一个case值对应，那么执行default后语句 。
    
```html
	<script type="text/javascript">
	var num = prompt("请输入1~12月份的数值:");
	switch(num) {
		case "1":
		case "3":
		case "5":
		case "7":
		case "8":
		case "10":
		case "12":
			console.log("31天");
			break;
		case "4":
		case "6":
		case "9":
		case "11":
			console.log("30天");
			break;
		case "2":
			var y = parseInt(prompt("请输入年份的数值:"));
			if(y%4==0 && y%100!=0 || y%400==0) {
				console.log("29天");
			} else {
				console.log("28天");
			}
			break;
		default:
			console.log("输入的月份是错误的");
			break;
	}
	</script>
```