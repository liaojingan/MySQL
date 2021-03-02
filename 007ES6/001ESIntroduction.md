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
    Nodejs环境搭建
    
    Node.js 是一个基于Chrome V8引擎的JavaScript运行环境。Node.js使用了一个事件驱动、非阻塞式
    I/O的模型，使其轻量又高效。Node.js的使用包管理器npm来管理所有模块的安装、配置、删除等操作，使
    用起来非常方便，但是想要配置好npm的使用环境还是稍微有点复杂

    使用node.js环境（相当于Python解释器，javascript运行时的环境）
    安装参考链接：https://jingyan.baidu.com/article/48b37f8dd141b41a646488bc.html
    1、下载安装node_Windows_x64.msi，只需要修改安装目录，其余默认下一步安装
    
    2、cmd命令窗口输入：node -v 和 npm -v查看是否安装成功
    
    3、因为默认情况下，NPM安装的模块并不会安装到NodeJS的程序目录，默认安装到C盘
    
       第一步修改NPM的缓存目录和全局目录路径，将对应的模块目录改到E盘nodejs的安装目录
        * 在D盘nodejs目录下创建两个目录，分别是node_cache和node_global，这是用来放安装过程的缓存文件以及最终的模块配置位置
        * 配置完成后，执行下面这两个命令：
          npm config set prefix "E:\nodejs\node_global"
          npm config set cache "E:\nodejs\node_cache"
          
    4、打开cmd命令行界面，在使用命令安装cluster模块
        * npm install cluster -g
        打开刚才创建的node_global目录，可以看到此时cluster目录就安装到这个目录底下
    
    
    5、然后配置npm的环境变量和nodejs的环境变量
        
        * 计算机图标上点右键，选属性，然后点击高级系统配置，弹出来的新窗口右下角有个环境路径，点击去，就能看到环境路径的配置界面
        * 点击新建用户变量，变量名填：NODE_PATH   变量值填：E:\nodejs\node_modules\ 点击确定就配置好NPM环境了
        
    6、此时还需要修改一些nodejs默认的模块调用路径，因为模块的安装位置变了，如果nodejs的命令还到原来的位置去找，肯定是找不到安装的模块了
    
        我们在环境变量窗口（不是系统变量），选择Path，然后点击右下角的编辑，然后选择npm那个。
        点击右边的编辑，将其修改为：E:\nodejs\node_global 点击确认保存
        
    7、打开一个新的cmd窗口。先输入命令：node进入nodejs的交互式命令控制台
        输入：require('cluster')如果能正常输出cluster模块的信息，说明上面的所有配置就算生效了
        
    8、将npm的模块下载仓库从默认的国外站点改为国内的站点，这样下载模块的速度才能比较快，只需要一个命令即可
        npm --registry https://registry.npm.taobao.org install cluster
        
        如果想一直使用这个源的地址，那么可以使用下面这个命令来配置
        npm install -g cnpm --registry=registry_url
        registry_url指的是国内提供的一些npm仓库地址，常用的有：
        https://registry.npm.taobao.org
        http://r.cnpmjs.org/
        
    VSCode环境搭建
        参考链接：https://www.cnblogs.com/xuhuale/p/10167159.html
        或者直接安装Run code插件，然后右键选择run code执行文件即可
    
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