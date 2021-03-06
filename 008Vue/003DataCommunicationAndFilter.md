### 子传父（组件数据通信）

    * 实现效果：单击按钮实现文字字号变为原来的一倍    
    
        1、父组件使用子组件Vcontent绑定自定义属性
        2、子组件native表示给button绑定原生事件
        3、触发父组件的自定义事件，然后将this.a传入到changeHandler(data)函数中
        4、传入的this.a触发这个方法
        
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .head {
            height: 200px;
            background-color: blue;
        }

        .content {
            height: 600px;
            background-color: red;
        }
    </style>
</head>

<body>
    <div id="app">
    </div>
    <script src="./nodejs/node_global/node_modules/vue/dist/vue.js"></script>
    <script>
        Vue.component("Vheader", {
            template: `
                <div class="head">
                    <Vbtn/>
                    <Vbtn/>
                </div> 
            `
        });
        // 下面子组件点击按钮绑定的事件
        Vue.component("Vbtn",{
            template: `
                <button>按钮</button>
            `
        });
        // App入口组件
        var App = {
            // 4、传入的this.a触发这个方法
            methods: {
                changeHandler(data) {
                    //console.log(this.msgFontSize);
                    this.msgFontSize += 1;
                    console.log(data);
                }
            },
            data() {
                return {
                    msg: "Hello Vuejs",
                    arr:[
                        {
                            id: 1,
                            name: "苹果",
                            price: 5,
                            place: "shanxi"
                        },
                        {
                            id: 2,
                            name: "香蕉",
                            price: 3,
                            place: "hainan"
                        }
                    ],
                    // 原始字号的一倍
                    msgFontSize: 1
                }
            },
            template: `
                // 作用到样式中
                <div :style="{fontSize:msgFontSize+'em'}">
                    <Vheader/>
                    <!-- 1、父组件使用子组件Vcontent绑定自定义属性-->
                    <Vcontent v-bind:msg='"msg"' :arr="arr" @change="changeHandler"/>
                </div>
            `,
            components: {
                // Vcontent子组件
                Vcontent: {
                    template:`
                        <div class="content">
                            我是内容组件
                            {{msg}}
                            <ul>
                                <li v-for="item in arr">{{item.name}}--{{item.price}}</li>
                            </ul> 
                            // 2、子组件native表示给button绑定原生事件
                            <Vbtn @click.native="changeFont"/>
                        </div> 
                    `,
                    // 子要声明props:['属性']接受
                    props:["msg","arr"],
                    data() {
                        return {
                            a: 100
                        }
                    },
                    methods: {
                        changeFont() {
                            console.log(123);
                            // 3、触发父组件的自定义事件，然后将this.a传入到changeHandler(data)函数中
                            this.$emit("change",this.a);
                        }
                    }
                }
            }
        };
        new Vue({
            el: "#app",
            template: `
                <App/>
            `,
            components: {
                App
            }
        });
    </script>
</body>

</html>
```

### 过滤器

    可以理解为是一个函数
    全局过滤器实例：将price价格数值前面加上符号“$”
    
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
    </style>
</head>
<body>
	<!-- 视图--HTML结构 -->
	<div id="app">	
	</div>
    <script src="./nodejs/node_global/node_modules/vue/dist/vue.js"></script>
    <script>
    	// 全局过滤器，第一参数为过滤器名称，第二个参数为函数
    	// 函数中第一个参数为原有的值val，第二个为传来的参数arg1
    	Vue.filter("addCurrency", function(val, arg1){
    		// 原来的数值加上要拼接的数值
    		return arg1 + val;
    	});
    	var App = {
    		data() {
    			// 需要返回数据对象使用return
    			return {
    				price: 0
    			}
    		},
    		template: ` 
    			<div>
					<input type="text" v-model="price"/>
					<!-- 加上管道符表示左边的数据用右边的函数过滤后才显示即填入参数名称addCurrency -->
					<p>{{price | addCurrency("$")}}</p>
				</div>
    		`
    	};
		new Vue( {
			el: "#app",
			// template模板优先渲染
			template: ` 
				<App></App>
			`,
			// 声明
			components: {
				App
			}
		});
    </script>
</body>
</html>
```

    局部过滤器，只能在组件中使用
    实例：将price的小数点过滤成整数输出
   
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
    </style>
</head>
<body>
	<!-- 视图--HTML结构 -->
	<div id="app">	
	</div>
    <script src="./nodejs/node_global/node_modules/vue/dist/vue.js"></script>
    <script>
    	// 全局过滤器，第一参数为过滤器名称，第二个参数为函数
    	// 函数中第一个参数为原有的值val，第二个为传来的参数arg1
    	Vue.filter("addCurrency", function(val, arg1){
    		// 原来的数值加上要拼接的数值
    		return arg1 + val;
    	});
    	var App = {
    		data() {
    			// 需要返回数据对象使用return
    			return {
    				price: 0
    			}
    		},
    		template: ` 
    			<div>
					<input type="text" v-model="price"/>
					<!-- 加上管道符表示左边的数据用右边的函数过滤后才显示即填入参数名称addCurrency -->
					<p>{{price | addCurrency("$")}}</p>
					<p>{{price | handleData}}</p>
				</div>
    		`,
    		// 不同的功能使用不同的过滤器，所以使用对象
    		filters: {
    			handleData: function(val) {
    				// 局部过滤器将传入的小数价格过滤成整数输出
    				return parseInt(val);
    			}
    		}
    	};
		new Vue( {
			el: "#app",
			// template模板优先渲染
			template: ` 
				<App></App>
			`,
			// 声明
			components: {
				App
			}
		});
    </script>
</body>
</html>
```