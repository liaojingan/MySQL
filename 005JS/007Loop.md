循环

    while循环、 do while循环、 for循环
    
	       while(循环条件) {
	           // 循环体------需要重复的语句
	       }

	       执行流程 1 先判断循环条件
	                2 假如条件为真，则执行循环体后继续回到1
	                  假如条件为假，整个while结束

	       死循环指的是条件永远成立           

```html
//打印1-100
<script type="text/javascript">
	var i = 1;
	while(i<=100) {
		console.log(i);
		i++;
	}
</script>
```

```html
<script type="text/javascript">
    // 页面上输出10个* 每一次输出一个
	var i = 1;
	while(i<=10) {
		document.write("*");
		i++;
	}
</script>
```

```html
<script type="text/javascript">
// 输出1-100之间所有能被3整除又能被8整除的数
// 注意i++的位置
	var i=1;
	while(i<=100) {
		if(i%3==0 && i%8==0) {
			console.log(i);
		}
		i++;
	}
</script>
```

```html
<script type="text/javascript">
	var sum = 0; i =1;
	while(i<=100) {
		sum += i;
		i++;
	}
	alert("sum的值是:"+sum);
</script>
```


        do {
	       循环体
        } while(条件);

        先执行循环体,判断条件，假如条件为真继续执行循环体，直到条件为假do-while循环结束
          
        while的循环体可能一次也不执行 do-while循环体至少执行一次 
	 
```html
<script type="text/javascript">
	var i=1;
	do{
		document.write(i," ");
		i++;
	} while(i<=10);

</script>
```

      打印1-10
            for(表达式1;表达式2;表达式3) {
                // 循环体
            }
             表达式1------变量初始化
             表达式2------循环条件
             表达式3------循环变量改变

	     执行流程: 1 先执行表1
	               2 执行表2,表2为假 for循环结束 表2为真执行第3步
	               3 执行循环体
	               4 执行表3 再回到第2步 

    下面三种书写的格式都是可行的

```html
<script type="text/javascript">
	for(var i=1; i<=10; i++) {
		document.write(i," ");
	}

	var i=1;
	for(; i<=10; i++) {
		document.write(i," ");
	}

	var i=1;
	for(; i<=10; ) {
		document.write(i," ");
		i++;
	}
</script>
```

总结：

    while  do-while for
	* 本质都是重复执行语句
    * while 一般只知道条件，不知道具体的循环次数情况下
	* do-while 希望有的代码一开始就执行一次 
	* for循环一般用于循环次数固定的情况

循环应用

```html
<script type="text/javascript">
	// 水仙花数  三位数 每个位的数的立方和等于它本身 
	// 编程实现得到所有的水仙花数
	for(var i=100; i<=999; i++) {
		var dig = i%10; //234
		var ten = parseInt(i%100/10);
		var hund = parseInt(i/100);
		if(Math.pow(dig,3) + Math.pow(ten,3) + Math.pow(hund,3) === i) {
			document.write(i+"<br>");
		}
	}
</script>
```

```html
<script type="text/javascript">
	// 求5! 1*1*2*3*4*5
	sum = 1;
	for(var i=1; i<=5; i++) {
		sum = sum*i;
	}
	alert("sum的值："+sum);
</script>
```

```html
<script type="text/javascript">
	// 1!+2!+3!+4!+5! 1！+ 1！*2 + 2！*3+3！*4+4！*5
	var i = 1;
	var sum = 0;
	for(var j=1; j<=5; j++) {
		i = i * j;
		sum = sum+i;
	}
	alert(sum);
</script>
```

```html
<script type="text/javascript">
// 1-1/2+1/3-1/4+....1/100求和  1/1+(-1)/2+1/3+(-1)/4+...(-1)/100
	var sum = 0;
	for(var i=1; i<=100; i++) {
		if(i%2==0) {
			sum += 1/i;
		} else {
			sum += (-1)/i;
		}
	}
	alert(sum);
</script>
```

break和continue用法

    break一般用于循环或switch结构,continue只用于循环,结束本次循环 继续下一次循环
    
```html
<script type="text/javascript">
	var i = 1;
	while(i<8) {
		console.log(i);
		i++;
		if(i==5) {
			break;
		}
	} // 1 2 3 4
</script>
```

```html
<script type="text/javascript">
	var i = 1;
	while(i<8) {
		console.log(i);
		i++;
		if(i==5) {
			continue;
		}
		console.log("打印成功");
	} 
//4后面不打印字符串"打印成功"
</script>
```

循环嵌套

```html
<script type="text/javascript">
	   /*
         ***** 
         *****
         *****
         *****
         ***** 
	   */
	//控制行数
	lines = prompt("请输入你需要的行数：");
	stars = prompt("请输入你需要打印的星星个数：");
	for(var i=1; i<=lines; i++) {
		//控制一行打印"*"的个数
		for(var j=1; j<=stars; j++) {
			document.write("*");
		}
		document.write("<br>");
	}   
</script>
```

```html
<script type="text/javascript">

	/*
        *       1      1
        **      2      2
        ***
        ****
     	*****
	*/

	for(var i=1; i<=5; i++) {
		for(var j=1; j<=i; j++) {
			document.write("*");
		}
		document.write("<br>");
	}
</script>
```

```html
/*
     ******
     *****
     ****
     ***
     **
     *
 */
 <script type="text/javascript">
 	for(var i=0; i<5; i++) {
		for(var j=1; j<=5-i; j++) {
			document.write("*");
		}
		document.write("<br>");
	}
</script>
```

```html
/*
       *
      ***
     *****
    *******
   ********* 
 */
 
<script type="text/javascript">
	for(var i=0; i<5; i++) {
		for(var j=1; j<=4-i; j++) {
			document.write("&ensp;");
		}
		for(var k=0; k<2*i+1; k++) {
			document.write("*");
		}
		document.write("<br/>");
	}
</script>
```

```html
	   /*
   
            打印九九乘法口诀表
            
            1*1=1
            1*2=2 2*2=4
            1*3=3 2*3=6 3*3=9
            ...
            1*9=9 ......................... 9*9=81          
	   */
	   
<script type="text/javascript">
	for(var i=1; i<=9; i++) {
		for(var j=1; j<=i; j++) {
			document.write(j+"*"+i+" = "+i*j,"&ensp;");
		}
		document.write("<br/>");
	}
</script>	    
```

