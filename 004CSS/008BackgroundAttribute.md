>1、背景色 
    
    background-color
    
>2、背景图

    注意定义背景图像、背景颜色等属性前先定义一个高度，因为浏览器默认给这些属性设置为0
    background-image: url("1.png")   背景图片
    background-repeat    repeat(默认铺满) | no-repeat（不平铺）| repeat-x（水平平铺） | repeat-y （垂直平铺）    背景平铺
    background-position  left  |  right  |  center  |  top  | bottom  背景定位
 
>3、背景定位(精灵图获取方式)
    
    background-position: 200px 200px; 第一个值是水平方向(正数向右，负数向左)，第二个值是竖直方向(正数向下，负数向上)
        表示让背景图向右移动200px , 向下移动200px
        还可用单词表示位置：
            【1】background-position: left; 只输入一个值另一个值默认为center 
            【2】background-position: left bottom; 输入两个值的时候，对顺序没有要求
            
        还可用百分号表示：
            background-position: 50% 0; 其中50%指的是图片的正中心跟盒子中心重合，需要会将50%转换为数值(盒子的宽度减去图片的一半)
**重点应用**： 小图标都做在一张图片上，减少对服务器的请求以及压力。css sprite css雪碧技术或css精灵图
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	<title>Document</title>
	<style type="text/css">
		div {
			/*盒子默认在左上角，要想图片下方的小图标放到盒子中就要往上移动，所以为负值*/
			width: 30px;
			height: 30px;
			background-image: url("img/1.png");
			background-position: no-repeat 0 -202px;
		}
	</style>
</head>
<body>
	<div></div>
</body>
</html>
```

>背景附属

    background-attachment: fixed;
    主要应用于：背景固定不动，文本随着滚动条滚动。