### 什么是ES6

    ECMAScript 6（简称ES6），又称ECMAScript2015(ES2015)
    2015年6月正式发布，是JavaScript语言的下一代标准
    
### 为什么要学

    更严谨的语法，更高效的编码
    更新的特性，更多的功能
    主流前端框架(Vue/React/Angular等)、大厂都在用ES6+
    兼容性解决方案成熟（Babel）Babel可以将ES6转换成低版本浏览器可以识别的语言
    
    新特性举例：箭头函数的使用场景——数组遍历
    
    let arr1 = [1,2,3]
    arr1.map(function (x) {
    return x * x;
    });
    
    简写为
    let arr2 = [1,2,3]
    arr2.map(x => x * x);
    
### 环境以及开发工具

    使用node.js环境（相当于Python解释器，javascript运行时的环境）
    下载安装node_Windows_x64.msi
    
    cmd命令窗口输入：node -v 查看是否安装成功
    
### ES6与JavaScript的关系

    JavaScript发展史
    
     1996年11月，Netscape将JavaScript提交给标准化组织ECMA
     1997年，ECMA发布ECMAScript1.0
     1999年12月，ECMAScript 3.0版发布，成为JavaScript的通行标准
     2011年6月，ECMAscript 5.1版发布，并且成为ISO国际标准（ISO/IEC 16262:2011） 
     截至 2012 年，所有浏览器都完整的支持ECMAScript 5.1，旧版本的浏览器至少支持ECMAScript 3 标准
     2015年6月17日，ECMAScript 6发布正式版本，即ECMAScript 2015
    
    ES6与JavaScript的关系
    
        ECMAScript 包含：JavaScript JScript ActionScript
        
### 常用的ES6新特性

     精简的箭头函数
       let sum = (a, b) => a + b
       
     严格的变量声明
       let age = 20  let声明变量
       const COURSE = “Python”  const声明常量
       
     更方便的解构赋值
       let [a, …b] = [1, 2, 3, 4]

     Promise容器实现异步编程
       new Promise((resolve, reject)=>{})