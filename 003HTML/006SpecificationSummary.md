>HTML规范总结

>1、type属性是否省略
```html
<!--之前，页面引入css和js文件需要使用如下方式：-->
<link rel="stylesheet" href="main.css" type="text/css">
<script src="main.js" type="text/javascript"></script>

<!--当前的标准是，type属性可以省略，使用方式如下：-->
<link rel="stylesheet" href="main.css">
<script src="main.js"></script>
```

>2、单引号和双引号的选择
>>在页面中，用到引号的地方统一推荐使用双引号
```html
<!--不推荐使用如下方法-->
<div id='news'></div>

<!--推荐使用如下方法-->
<div id="news"></div>
```

>3、标签和标签属性大小写
>>HTML中标签和标签属性统一使用小写的形式，固有属性值也使用小写；只有自定义的属性值可以没有限制
```html
<!--不推荐使用如下方式-->
<input type="BUTTON">
<DIV>html规范</DIV>

<!--推荐使用如下方式-->
<input type="button">
<div>html规范</div>
```

>4、代码的注释
>>如果可能尽量不写注释，尽可能减少文档的体积；如果必须添加注释，则要遵循如下规则

    (1)详尽解释，解释代码解决问题、解决思路、是否为新鲜方案等。
    (2)模块注释，github建议不使用模块结束注释。
    (3)特别说明：注释文本与两端（-）之间要有一个空格。
    (4)待办注释：<!--TODO:待办事项-->
```html
<!--导航栏模块-->

<div class="nav">

</div>

<!--/导航栏模块-->
```

>5、HTML的布尔属性值
>>HTML5规范中：disabled、checked、selected等属性不用设置值。
```html
<input type="text" disabled>
<input type="checkbox" value="12" checked>

<select>
    <option value="广东" selected>广东</option>
    <option value="深圳">深圳</option>
</select>
```

>6、同一个文档中避免出现重复的id属性值（保证唯一性）