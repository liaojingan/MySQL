```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
	<script type="text/javascript">
	    // 1 计算数组中所有偶数的和和奇数的和 并且统计偶数和奇数个数

	    function getCount(arr) {
            var oddSum = 0;  // 记住奇数的和
            var oddCount = 0;// 统计奇数个数 
            for(var i=0, len=arr.length; i<len; i++) {
            	if (arr[i]%2) {
            		oddSum += arr[i];
            		oddCount++;
            	}
            }
            console.log("所有奇数之和"+oddSum);
            console.log("所有奇数个数"+oddCount);
	    }

	    var arr = [12,4,5,7,11,2,3];
	    getCount(arr);

	    // 2 输出数组中最大值和最小值
	    function getValue(arr) {
           // 定义一个数组 存最大值和最小值
           var res = [];
           var max = arr[0];// 默认值
           var min = arr[0];
           for(var i=1, len=arr.length; i<len; i++) {
           	    if (arr[i]>max) {
           	    	max = arr[i];
           	    }
           	    if(arr[i]<min) {
           	    	min = arr[i];
           	    }
           }
           res[0] = max;
           res[1] = min;
           return res;
	    }

	    var arr = [-1,10,2,-5,19];
	    var res = getValue(arr);
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
	<title>Document</title>
</head>
<body>
	
	<script type="text/javascript">
	   // api application interface 应用程序接口
	   // 数组的增加与删除
	   /* push()    在数组的末尾添加一个或多个元素
          unshift()  .......前面。。。。。。 
          以下两个方法表示删除,它们返回值是删除的元素
          pop()     在数组的末尾删除一个元素
          shift()   .......前面。。。。。 
	   */
       
       
	   var numbers = [1,2,3,4,5];
	   //numbers[5] = 6;
	   //numbers[numbers.length] = 6;
	   numbers.push(6);
	   numbers.push(7,8);
	   numbers.unshift(-1,0);
	   console.log(numbers);
        
	   /*
            1 2 3  ------>  0  1 2 3
	   */
	   
	   var arr = [1,2,3];
	   for(var i=arr.length; i>=1; i--) {
	   	     arr[i] = arr[i-1];
	   }
	   arr[0] = 0;
	   console.log(arr);
	   

	   var arr1 = [1,3,5,7,9];
	   arr1.pop(); // 9
	   arr1.pop();
	   arr1.shift();
	   console.log(arr1);


	   // 在数组任意位置删除或添加元素 splice()
	   var arr = [1,2,3,4,5,6];
	   arr.splice(3,2); // 表示从索引3开始 删除2个元素
	   arr.splice(4,1);
	   arr.splice(3,0,3.5,3.8); // 从索引为3开始 添加多个元素
	   arr.splice(3,2,3.5,3.8,3.9); // 从索引为3开始替换后两个元素，3.9依然添加到后面
	   console.log(arr); // [1,2,3,6]
	</script>		
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
	<script type="text/javascript">
	    // concat 表示数组连接其他值  不改变原数组
	    var arr1 = [1,2,3,4];
	    var arr2 = [5,6,7,8];
	    var res = arr2.concat(arr1,9);
	    console.log(res);

        // 迭代器方法
        function isEven(x) {
        	console.log(x);
        	return x%2===0?true:false;
        }
        var numbers = [1,2,3,4,5,6];
        // every方法会迭代数组中每个元素  直到遇到返回false
        numbers.every(isEven);

        // some基本与every行为类似,会迭代数组每个元素 直到遇到返回为true结束
        numbers.some(isEven);

         /* forEach 与for循环结果相同
         numbers.forEach(function(x) {
             console.log(x);
         });
         */

         //map
         var res1 = numbers.map(isEven);
         console.log(res1); // [false, true, false, true, false, true]
         
         // filter 返回一个新数组 新数组由函数返回true的元素组成
         var res2 = numbers.filter(isEven);
         console.log(res2); // [2, 4, 6]
         

         // reduce
         var sum = numbers.reduce(function(prev,current,index,array) {
             console.log(prev,current);
             return prev+current;
         });
         alert(sum);

         // 一开始prev代表1  current代表2
         // prev会利用上一次函数返回值
         // 1 2
         // undefined 3
         // undefined 4
         // undefined 5
         // undefined 6
         // function fn() {

         // }

         // alert(fn());
 
         // 1   2  返回3
         //   3    3 返回6
         //   6     4
         //   10      5
         //   15        6 返回21 最后一次返回值会作为整个reduce的返回值
	</script>
</body>
</html>
```


```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
	   // 逆序  reverse()
	  /* var arr = [1,2,3,4,5];
	   arr.reverse();
	   console.log(arr);*/

	   // 排序   "7"  "4"  "10" "3"  "6"
	   // sort 按字符编码进行排序，要按数值大小对数字进行排序，就使用排序函数
	   var arr = [7,4,10,3,6];
	   arr.sort(function(a,b) {
	   	   //return a-b; 升序排序
	   	   if(a<b) {
	   	   	  return 1; 
	   	   } else if(a>b) {
	   	   	  return -1
	   	   }
	   	   return 0;
	   	});
	   console.log(arr); // [10, 3, 4, 6, 7]

	   // 搜索
	   var arr2 = [10,9,12,4,4,56];
	   var num = 4;
	   // 返回搜索到的第一个数字4的索引号
	   var index = arr2.indexOf(num);
	   // 返回搜索到的最后一个数字4的索引号
	   var index2 = arr2.lastIndexOf(num);
	   alert(index2);
	</script>
</body>
</html>
```

数组应用详解

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
	<script type="text/javascript">
         // 编写函数  has(arr,44)  判断某个元素是否存在数组中 存在返回true 不存在返回false
         function has(arr,num) {
         	 for(var i=0; i<arr.length; i++) {
         	 	if (arr[i] === num) {
         	 		return true;
         	 	}
         	 }
         	 return false; // 注意返回false的位置
         }

         /*var arr = [13,45,23,5,6];
         alert(has(arr,23)); */
         // 编写函数 norepeat(arr) 去掉数组中重复的元素 返回新的数组
         //  [34,12,5,12,56] -----> [34,12,5,56]
         // 方法一 从头到尾对每一个元素进行判断 不在新数组中就加入新数组
         function norepeat(arr) {
         	 var newArr = [];
         	 //var j = 0;// 从下标为0开始赋值
         	 for(var i=0, len=arr.length; i<len; i++) {
         	 	 if (!has(newArr,arr[i])) {
         	 	 	// 原数组元素不在新数组中就添加
         	 	 	newArr.push(arr[i]);
         	 	 	//newArr[j++] = arr[i];
         	 	 	//newArr[newArr.length] = arr[i];
         	 	 }
         	 }
         	 return newArr;
         }
         
         // 方法二 针对有序的数组 [1,1,2,3,3,24]
         function norepeat2(arr) {
            var newArr = [];
            for(var i=0; i<arr.length; i++) {
            	if (arr[i] != arr[i+1]) {
            		newArr.push(arr[i]);
            	}
            }
            return newArr;
         }

         //var arr = [2,4,56,23,4,2,10];
         /*var arr = [1,1,2,3,3,24];
         var res = norepeat2(arr);
         alert(res);// [2,4,56,23,10]*/


         // 假如有个排序好的数组 现在插入一个数 按原来的规律
         // [6,8,11,13] 9  新数组[6,8,9,11,13]
         // 找到添加数的下标
         function fnInsertArr(arr,num) {
         	 var index = arr.length;  // 记住添加数的下标
         	 for(var i=0, len=arr.length; i<len; i++) {
         	 	  if (arr[i]>num) {
                      index = i;
                      break;
         	 	  }
         	 }
         	 // 把num插入到index位置处
         	 arr.splice(index,0,num);
         	 return arr;  //一定要return，返回值，否则就是undefined
         }

         var arr = [6,8,11,13];
         var res = fnInsertArr(arr,10);
         alert(res);

        // join() 数组转成字符串
	   var numbers = [1,2,3,4,5];
	   var res = numbers.join(":");
	   //console.log(typeof res);
	   console.log(res);
	   console.log(numbers.toString());
         
	</script>
</body>
</html>
```

二维数组和多维数组

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>

	<script type="text/javascript">
	    // //  3排3列
	    //var students = [[1,1],[1,2],[1,3],[2,1],[2,2],[2,3],[3,1],[3,2],[3,3]];
	    // 2排2列
	    var students = [[1,1],[1,2],[2,1],[2,2]];
	    //console.log(students[0][0]);
	    // i代表第几个人
	    for(var i=0; i<students.length; i++) {
             // students[i] 又是一个数组
             //console.log(students[i]);
             for(var j=0; j<students[i].length; j++) {
             	document.write(students[i][j]);
             }
             document.write("<br/>");
 	    }
	</script>
	

</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
	   // 排序 
	   var arr = [10,4,12,-2];
	   function bubbleSort(arr) {
	   	   	// 定义一个循环 控制轮数  arr.length-1 
	   		for(var i=0; i<arr.length-1; i++) {
	   	  		// 定义一个循环 控制每相邻两个数比较
	   	  		for(j=0; j<=arr.length-2-i ;j++) {
	   	  			if (arr[j] > arr[j+1]) {
	   	  				var temp = arr[j];
	   	  				arr[j] = arr[j+1];
	   	  				arr[j+1] = temp;
	   	  			}
	   	  		}
	      }
	   }  
	   bubbleSort(arr);
	   alert(arr);
	</script>
</body>
</html>
```

数组已经排序完成了，但是按上面的代码来看，数组还会继续排序，所以我们加一个标志位，如果某次循环完后，没有任何两数进行交换，就将标志位 设置为 true，表示排序完成，这样我们就可以减少不必要的排序，提高性能。

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
         function bubble(arr4) {
             var len = arr4.length-1;
             for(i=0; i<len; i++) {
                var flag = true;
                for(j=0; j<len-i; j++) {
                    if(arr4[j]>arr4[j+1]) {
                        var temp = arr4[j];
                        arr4[j] = arr4[j+1];
                        arr4[j+1] = temp;
                        flag = false;
                    }
                }
                if(flag) {
                    break;
                }
             }
             return arr4;
         }

         var bubbleNum = [22,334,55,677,11,-1];
         var res3 = bubble(bubbleNum);
         console.log(res3); 
	</script>
</body>
</html>
```
