### 变量

     声明变量
    var a = 100
    let b = 'hello'
    
### let的三大特性（为什么要使用let）

     特征一：不存在变量提升，必须要先声明，再使用
       console.log(a); // 报错ReferenceError
       let a = 2;
       
     特征二：不能重复声明
       let b = 100
       let b = 'hello' // 报错 SyntaxError
       
     特征三：块级作用域，变量只在代码块内有效
       function func() {
            let n = 5;
            if (true) {
                let n = 10;
            }
        console.log(n); // n = ？ 
        }