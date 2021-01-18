圆角边框
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style type="text/css">
		div:nth-child(1){
			width: 200px;
			height: 200px;
			border: 1px solid #000;
			border-radius: 20px;
			background-color: gold;
		}
		div:nth-child(2){
			width: 200px;
			height: 200px;
			border: 1px solid #000;
			border-radius: 100px;
			background-color: gold;
		}
		div:nth-child(3){
			width: 200px;
			height: 600px;
			border: 1px solid #000;
			border-radius: 100px;
			background-color: gold;
		}
		div:nth-child(4){
			width: 600px;
			height: 200px;
			border: 1px solid #000;
			border-radius: 20px 40px 60px 80px;
			background-color: gold;
		}
		div:nth-child(5){
			width: 600px;
			height: 200px;
			border: 1px solid #000;
			border-radius: 20px 60px 80px;
			background-color: gold;
		}
		 div:nth-child(5){
			width: 600px;
			height: 200px;
			border: 1px solid #000;
			/* border-radius: 20px;
			border-top-left-radius: 60px;
			border-top-right-radius: 60px;
			border-bottom-right-radius: 100px; */
			border-radius: 60px 60px 100px 20px;
		} 
		div:nth-child(6){
			width: 600px;
			height: 200px;
			background-color: yellowgreen;
			border-radius: 50%;
		}
		div:nth-child(7){
			width: 600px;
			height: 200px;
			background-color: yellowgreen;
			border-radius: 10% 20% 30% 80%;
		}
		div:nth-child(8){
			width: 600px;
			height: 200px;
			background-color: yellowgreen;
			border-radius: 0% 100%;
		}
		div:nth-child(9){
			width: 600px;
			height: 200px;
			background-color: yellowgreen;
			border-radius: 100% 0;
		}
		div:nth-child(10){
			width: 200px;
			height: 100px;
			border: 1px solid #000;
			background-color: skyblue;
			border-radius: 0px 0px 100px 100px;
		}
		div:nth-child(11){
			width: 100px;
			height: 200px;
			border: 1px solid #000;
			background-color: skyblue;
			border-radius: 0px  100px 100px 0px;
		}
		div:nth-child(12){
			width: 100px;
			height: 200px;
			border: 1px solid #000;
			background-color: green;
			border-top-left-radius: 50px 80%;
			border-top-right-radius: 50px 80%;
		}
	</style>
</head>
<body>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
</body>
</html>
```