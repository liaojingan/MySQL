>1、颜色属性

    颜色的表示方法(取色器：fascapture)：
        【1】直接写颜色的名称
                red、green、yellow、white、black、skyblue、brown、blue、pink、orange......
        
        【2】十六进制显示颜色
                0-9  a-f 表示的颜色越来越浅；
                值相同则可简写，比如 #888888 可写成#888
                黑：#000000；红：#ff0000；绿：#00ff00；蓝：#00000ff;
                
        【3】rgb 表示方法，括号里填写色值
                每种颜色取值：0~255
                红色：rgb(255,0,0)、绿色：rgb(0,255,0)、蓝：rgb(0,0,255)、白色：rgb(255,255,255)、黑色：rgb(0,0,0)、灰色(111,111,111)
        
        【4】rgba   a代表alpha 不透明度， 值0--1； 0表示完全不透明；0.5表示半透明
                color: rgba(120,120,120,0.5)
                
>文字属性

    1、font-size：文字大小，有单位，目前是px(还有移动端rem、em单位)
       比如文字设置大小为font-size: 20px; 
       
    2、chrome浏览器默认大小为12px;
    
    3、line-height：行高，会默认字体在行高中，垂直居中
       例如  font-size:16px;
            line-height:150%;(相对于字体大小，所以行高为字体的1.5倍即24px)
           
    4、color：文字颜色；

    5、font-family：字体
        常用“宋体"/"微软雅黑"
        比如:font-family: "微软雅黑","宋体";  （后面的字体为备用字体）
        font-family: "Arial",Microsoft Yahei","Simsum"（英文字体写在前面，中文写后面且加载速度比写中文块）   
        
       综合：font: 16px/32px "Simsum"; (字号、行高、字体)
       
>font-weight(默认是normal)

    font-weight:700;  等价于 font-weight:bold;    都是加粗效果
    font-weitht:400;  等价于 font-weight:normal;  表示正常字体
    作用：可以将h系列标题加粗的效果转换成正常的样式
    
**对h系列标签的作用：这个h系列标签给文字产生二级标题的含义，只不过说浏览器给它进行加粗显得重要些**

>font-style(字体样式，默认是normal)

    font-style: italic; 让字体倾斜(常用)
    font-style: normal; 不倾斜
    font-style: oblique 与italic区别在于oblique是普通的倾斜，italic会找到新的斜的字型替代 
    注意：中文一致使用italic
    
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	<title>Document</title>
	<style type="text/css">
		.iteam1 {
			font-style: italic;
			font-size: 40px;
		}

		li i {
			font-style: normal;
		}

		ul li.alone{
			font-style: oblique;
		}
	</style>
</head>
<body>
	<ul class="iteam1">
		<!-- 这里i标签起到钩子的作用，就可以单独对“拔毛”进行样式设置 -->
		<li class="alone">人走茶凉lilili</li>
		<li>雁过<i>拔毛</i></li>
		<li>魑魅魍魉lilili</li>
		<li>尸位素餐lilili</li>
	</ul>
</body>
</html>
```

>text-decoration(字符装饰)

    text-decoration: none;          默认值
    text-decoration: underline;     下划线
    text-decoration: line-through;  删除线
    text-decoration: overline;      上划线
    
    text-decoration: none;主要作用：删除超链接的下划线。
    
>综合写法

    font: italic 700 16px/32px Arial,sans-serif;
    相当于：
        font-style: italic;
        font-weight: 700;
        font-size: 16px;
        line-height: 32px;
        font-fmaily: Arial, sans-serif;
        
    一般综合只写后面四个：
    font: 16px/32px Arial,sans-serif;
    
>text-align(文本对齐方式)

    text-align: left;
    text-align: right;
    text-align: buttom;
    text-align: top;
    
>text-index(文本缩进方式)

    主要作用一：用来设置段落缩进
    .p1 {
        font-size: 20px;
        text-indent: 2em;   <!--2em表示对应文字大小的两倍，就可以缩进了。-->
    }
    
    主要作用二：使用文本缩进，比如在h1标题中写入“京东",再设置一个很大的文本缩进负值让它向左隐藏，即可放入图片，易于搜索引擎优化。，