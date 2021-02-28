数组对象的作用：

    使用单独的变量名来存储一系列的值

定义数组的方式一

```html
<script type="text/javascript">
	var arr1 = new Array();       //空数组
	var arr2 = new Array(8);      //8表示这个数组的元素个数
	var arr3 = new Array(3,4);    //该数组存放了两个数值3和4
	var arr4 = new Array("js","python","java");  //存放字符串 
	var arr5 = new Array("php",123,function() console.log(1),true);  //混合数据存储
</script>
```

定义数组的方式二

```html
<script type="text/javascript">
	var arr1 = [];  //空数组
	var arr2 = [9]; //有一个元素9，注意区分另一种方式
	var arr3 = [3,4,5,7,9]; //存多个数用逗号分隔
</script>
```

数组的属性length,数组的长度即数组元素的个数

```html
<script type="text/javascript">
	var arr1 = [];  //空数组
	var arr2 = [9]; //有一个元素9，注意区分另一种方式
	var arr3 = [3,4,5,7,9]; //存多个数用逗号分隔

	console.log(arr1.length);  //打印对应数组的长度
	console.log(arr3.length);

	arr3.length = 3;  //给数组规定存储的长度
	console.log(arr3.length[3]);  //超出数组存储长度，就为undefined 
</script>
```

数组元素的引用

```html
<script type="text/javascript">
	var arr = [12,34,56,775,34];
	console.log(arr[2]);
	console.log(arr[arr.length-1]);   //最后一个元素
	console.log(arr[5]);              //长度越界为undefined

	 // 用数组求斐波那契 前20项数
	 var fibonacci = [];
	 fibonacci[0] = 1;
	 fibonacci[1] = 1;

	 for(var i=2; i<=19; i++) {      //注意i=2
	 	fibonacci[i] = fibonacci[i-1] + fibonacci[i-2];
	 	console.log(fibonacci[i]);
	 }
	 
	 // 打印整个数组 数组的遍历(访问每一个元素)
	 // for(var i=0; i<=fibonacci.length-1; i++) {
	 // 	console.log(fibonacci[i]);
	 // }

	 for(var i=0, len = fibonacci.length; i<=len-1; i++) {
            console.log(fibonacci[i]);
     } 
</script>
```