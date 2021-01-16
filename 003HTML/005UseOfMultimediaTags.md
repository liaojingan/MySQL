>多媒体

    html4.01插入音视频 借助于flash
    
    视频： video标签(支持的格式mp4和ogv)
           提供js api(onpause监听暂停事件、onplay监听播放事件)
           方法：
                play() pause()
                
    音频： audio标签(支持的格式mp3和ogg)IE9开始兼容
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<!-- controls属性表示是否显示播放控件  autoplay表示视频打开自动播放-->
	<video src="../picture/p-call.mp4" controls autoplay></video>

	
	<!-- 此方法可以设置多个不同格式的视频，来保证兼容性 -->
	<video controls autoplay>
		<source src="p-call.mp4">
	</video>

    <!--音频-->
    <audio autoplay="autoplay" src="../picture/赵雷 - 成都.mp3" controls="controls"></audio>
</body>
</html>
```
