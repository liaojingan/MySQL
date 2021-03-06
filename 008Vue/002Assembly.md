### 事件

    vue是实现单页应用、移动端，页面切换主要是通过组件化，视图由框架维护、只关注数据
    vue的底层才操作DOM元素
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
	<!-- 视图--HTML结构 -->
	<div id="app">
		<!-- v-on指令为元素绑定事件处理函数 -->
		<button v-on:click="clickHander">点击</button>
		<!-- 语法糖简写形式 -->
		<button @click="clickHander2">点击</button>
	</div>
	<!-- 1、引入包 -->
    <script src="./nodejs/node_global/node_modules/vue/dist/vue.js"></script>
    <script>
    	// 2、创建vue实例
		let vm = new Vue({
			el: "#app",  //元素
 			data() {      //数据
				return {

				}
			},
			// 可能绑定多个方法，所以使用对象
			methods: {
				clickHander() {
					console.log("珍珍");
				},
				clickHander2() {
					console.log("哈哈哈哈");
				}
			}	
		});

		console.log(vm.msg);
    </script>
</body>
</html>
```

### vue计算器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
	<!-- 视图--HTML结构 -->
	<div id="app">
		<!-- v-model.number表示会将结果转换成数值 -->
		<input type="number" v-model.number="num1">
		<select name="" id="" v-model.number="operator">
			<option value="0">+</option>
			<option value="1">-</option>
			<option value="2">*</option>
			<option value="3">/</option>
		</select>
		<input type="number" v-model.number="num2">
		<button @click="cal">=</button>
		<!-- 结果值显示 -->
		<span>{{res}}</span>
	</div>
	<!-- 1、引入包 -->
    <script src="./nodejs/node_global/node_modules/vue/dist/vue.js"></script>
    <script>
    	// 2、创建vue实例
		var vm = new Vue({
			el: "#app",  //元素
 			data() {      //数据
				return { 
					num1: 0,
					num2: 0,
					operator: 0,
					res: 0
				}
			},
			methods: {
				cal() {
                    // 拿到两个操作数
                    //console.log(this.num1,this.num2,this.operator);
                    switch (this.operator) {
                        case 0:
                            this.res = this.num1 + this.num2;
                            break;
                        case 1:
                            this.res = this.num1 - this.num2;
                            break;
                        case 2:
                            this.res = this.num1 * this.num2;
                            break;
                        case 3:
                            this.res = this.num1 / this.num2;
                            break;
                    }
				}
			}
		});
    </script>
</body>
</html>
```

### 组件和全局组件
    全局组件又称为公共组件（一般页面上导航栏、按钮等定义成全局组件）
    
    组件化开发：体现封装的思想，即对视图的封装；代码量减少，维护方便哪个地方出问题找哪块代码
    比如京东网页，可以将导航栏、侧边栏、底部等封装成组件
    
    * 全局组件
    
        1、全局组件声明后即可使用，不需要挂载
        2、template表示结构模板，渲染的是组件模板
        3、使用 （当做标签来使用）
        4、template需要一个根元素，否则只会展示模块中的第一个标签元素
        5、组件本质上就是vue实例
        
        流程：1、声明组件；2、使用组件
        
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
	<!-- 视图--HTML结构 -->
	<div id="app">
		<!-- 2、使用 （当做标签来使用），挂载组件起什么名称，使用标签就用什么名称，注意全局的不需要挂载-->
		<Vheader></Vheader>
	</div>
    <script src="./nodejs/node_global/node_modules/vue/dist/vue.js"></script>
    <script>
    	// 全局组件
    	// component传入第一个参数组件名一般大写，第二个参数为对象，是对组件的描述（可以有数据、行为或结构）
    	Vue.component("Vheader", {
    		// template表示结构模板，``使用模板字符串
    		// 1、声明组件，注意template需要一个根元素
    		template: `
    			<div>
				<div>我是头部</div>
				<div>123</div>
				<p @click="handler">{{num}}</p>
				</div>
    		`,
    		// 函数
    		data() {
    			return {
    				num: 100
    			}
    		},
    		// 方法
    		methods: {
    			handler() {
    				alert("test")
    			}
    		}
    	});
		new Vue({
			el: "#app",  //元素
 			data() {      //数据
 				return {

 				}
			},
			methods: {
				
			}
		});
    </script>
</body>
</html>
```

    * 局部组件
    
        1、只能在当前实例中使用
        2、嵌套组件，比如导航栏为一个组件，里面包含的登录作为一个子组件
        
        流程：1、声组；2、挂组；3、用组
        
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
	<!-- 视图--HTML结构 -->
	<div id="app">
		<!-- 3、使用 （当做标签来使用），挂载组件起什么名称，使用标签就用什么名称，注意全局的不需要挂载-->
		<Vheader></Vheader>
		<Vheader></Vheader>
	</div>
    <script src="./nodejs/node_global/node_modules/vue/dist/vue.js"></script>
    <script>
    	// 局部组件
    	// 1、声明组件
    	var Vheader = {
    		template: `
				<div>头部</div>
    		`,
    		data() {
    			return {

    			}
    		},
    		methods: {

    		}
    	};
		new Vue({
			el: "#app",  //元素
 			data() {      //数据
 				return {

 				}
			},
			methods: {
				
			},
			// 使用上面结构模板将组件放到div中,加-s表示可以放多个组件
			// 2、挂载组件
			components: {
				// Vheader这是组件名称，可以任意写，一般名称和组件名称一致就好，相同情况下可以只写Vheader
				Vheader
			}
		});
    </script>
</body>
</html>
```

### 父传子数据（组件数据间通信）

    整个页面不可能说头部、侧边栏、主体组件等都发送请求，所以可以使用包含这些组件的父组件进行发送
    
    * 一定要先声明子组件，下面才定义父组件使用
    * 多个子组件要加上根元素div
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
    	.head {
    		height: 200px;
    		background-color: red;
    	}

    	.main {
    		height: 200px;
    		background-color: blue;
    	}
    </style>
</head>
<body>
	<!-- 视图--HTML结构 -->
	<div id="app">
		<App></App>		
	</div>
    <script src="./nodejs/node_global/node_modules/vue/dist/vue.js"></script>
    <script>
    	// 组件必须要先声明，才能写下面的代码使用组件
    	var Vheader = {
    		template: ` 
				<div class="head"></div>
    		`
    	};
    	var Vmain = {
    		template: ` 
				<div class="main"></div>
    		`
    	}
    	// 定义App为父组件（入口组件），里面包含下面的两个组件
    	var App = {
    		// 放入子组件，注意加上根元素div
    		template: ` 
    			<div>
    			<Vheader></Vheader>
    			<Vmain></Vmain>
    			</div>
    		`,
    		components: {
    			Vheader,
    			Vmain
    		}
    	}
    	
    	// 实例可以理解为是最大的组件
		new Vue({
			el: "#app",  //元素
 			components: {
 				// 这里只需要填写入口组件
 				App
 			}
			
		});
    </script>
</body>
</html>
```

    * 想要data数据在Vheader和Vmain中使用，如下
        1、父组件中哪一个组件需要数据就在哪一个组件上绑定元素
        2、子组件通过props来接收传入的数据，props可以是数据，表示可以接收多个参数
        3、模板中使用数据
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
    	.head {
    		height: 200px;
    		background-color: red;
    	}

    	.main {
    		height: 200px;
    		background-color: blue;
    	}
    </style>
</head>
<body>
	<!-- 视图--HTML结构 -->
	<div id="app">
		<App></App>		
	</div>
    <script src="./nodejs/node_global/node_modules/vue/dist/vue.js"></script>
    <script>
    	// 组件必须要先声明，才能写下面的代码使用组件
    	var Vheader = {
    		template: ` 
				<div class="head"></div>
    		`
    	};
    	var Vmain = {
    		// 3、模板中使用数据
    		template: ` 
				<div class="main">
					{{msg}}
				</div>
    		`,
    		// 2、子组件通过props来接收传入的数据，props可以是数据，表示可以接收多个参数
    		props: ["msg"]
    	}
    	// 定义App为父组件（入口组件），里面包含下面的两个组件
    	var App = {
    		// 放入子组件，注意加上根元素div
    		// 1、哪一个组件需要数据就在哪一个组件上绑定元素
    		template: ` 
    			<div>
    				<Vheader></Vheader>
    				<Vmain msg="msg"></Vmain>
    			</div>
    		`,
    		// 添加数据
    		data() {
    			return {
    				msg: "vuejs"
    			}
    		},
    		components: {
    			Vheader,
    			Vmain
    		}
    	}
    	
    	// 实例可以理解为是最大的组件
		new Vue({
			el: "#app",  //元素
 			components: {
 				// 这里只需要填写入口组件
 				App
 			}
			
		});
    </script>
</body>
</html>
```
