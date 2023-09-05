---
layout: post
title: "vue笔记"
author: "GG Bond"
tags: Tutorial
excerpt-separator: "vue一点点笔记"
---

## Steps

### vue
* 渐进式框架：
渐进式意味着你可以将Vue作为你应用的一部分嵌套其中
	Vue-首页-详情-分类
	vue的核心只有20kb左右，如果你希望更多的业务逻辑使用vue来实现，那么vue核心库以及周边的生态系统可以帮我们扩展使用 vue-router vuex
* Vue的优点：易用 灵活 高效
* Vue的特点：
	1.数据驱动
	2.组件系统
* Vue的注意事项：
	Vue不支持IE8及以下浏览器，因为Vue中使用了IE8无法模拟的ECMAScript5新特性
	也就意味之Vue支持所有兼容ECMAScript5特性的浏览器
* Vue的引入方式：
	1.下载vue.js 在script中引用本地文件
	2.直接使用CDM链接形式，引入文件
	3.npm下载安装Vue
	4.使用命令行工具（vue-cli）安装
	开发版：vue.js 300KB
	生产版：vue.min.js (压缩版)90KB

### 响应式数据，数据发生更改，页面视图也随着改变，页面如果发生更改，数据同样会随之改变

### Vue是一个MVVM框架
	* MVC框架   MVVM框架   MVP框架
### MVC  单向数据流
	* m:model  数据层（模型层）
		处理数据逻辑，负责在数据库中存取数据等操作
	* v:view  视图层
		处理数据显示的部分
	* c:controller  控制器
		试图与数据的交互部分，通常都需要控制器负责从数据曾拿到数据，在视图层渲染，控制用户输入内容，将用户输入的内容拿到传递给数据层
### MVVM 双向数据流
	是由微软提出的一个双向数据流框架,M:model数据层,V:view视图层,VM:view-model视图模型层，vm通过数据绑定将数据从model发送给view，再通过DOM监听从view获取用户的操作改变model；
	MVVM将model用于纯js对象表示，view就负责视图，两者做到最大程度的分类
	* M     model
	* V      view
	* VM   view-model  视图模型层：通过数据绑定来将数据渲染到视图层，再通过DOM监听，去监听视图层变化，视图层一旦发生变化，则将变化的内容发送给数据层
	*设计理念：让开发者只需要关注Midel层的变化，阳MVVM框架去自动更新DOM状态，从而把开发者从操作DOM的繁琐步骤中解脱出来
### Vue的响应式原理（重点）
	vue.js是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个数据的setter和getter，在数据变动时发布消息给订阅者，触发相应监听回调来渲染视图
	* 具体步骤：
		1.需要observer（观察者）对数据对象上的各个数据进行递归遍历，然后将这些数据都加上getter和setter方法
		2.compile（模板解析器）解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动
		就会收到通知，从而更新视图
		3.watcher（订阅者）是observer和compile之间的通信桥梁
		4.MVVM框架作为数据绑定的路口，去整合observer、compile、watcher三者，通过observer监听自己的model数据变化，通过compile来解析编译模板指令，渲染view层，然后
		通过watcher搭起observer和compile之间的桥梁，达到最终的效果，数据变化-->视图更新，视图交互变化-->数据model的双向绑定效果
### getter和setter
	在每一个对象中都会有两个存储器属性，分别是get和set，这两个属性对应的方法就是getter个setter，在setter函数中一切的return都是无效的
### Object.defineProprety()
	
		
Jquery是一个JS的函数库
### 框架：封装一些与业务逻辑无关的重复性代码，形成框架

### Vue中的插值表达式（重点）：
	Mustache语法(胡须语法、小胡子语法)：{{}}；    主要作用：渲染数据
	在该语法中可以写：变量（常用）、字符串、数值、布尔值、表达式、方法
### Vue中的指令（重点）：
	* 什么是指令：在vue中，标签上出现的以v-开头的标签属性，都是属于vue中的指令，作用是通过指令能够快速操作DOM
	1.v-once：只会初始渲染一次数据，渲染完之后，该标签里面的数据不再进行响应式改变
	2.v-html：可以解析数据中的html代码，该标签内原有的内容会被替换掉
	3.v-text：不会解析html代码，该标签内原有的内容会被替换掉
	4.v-pre：不对具有v-pre属性的标签内容做解析，不会解析{{}}
	5.v-cloak：解决浏览器刷新时页面插值闪烁问题，在vue实例加载完之前，div上面会有一个v-cloak属性，当vue实例加载完之后，该属性会删除，然后我们可以利用css属性选择器对div进行样式的控制
	6.v-bind：是动态修改标签的属性 简写成:src（语法糖）
		* 绑定class属性语法：
			1.字符串：表示将该字符串作为class名使用
			2.数组：在标签上存在多个类名时可以使用，每一个数组项都表示一个class名
			3.对象：对象的属性名是是否要添加的class类名，属性值是Boolean类型的值，可以决定该类名是否要加入到标签中，如果为true则添加类，反之移除类；作用：当一个类需要动态添
			加或删除时，可以使用
		* v-bind动态绑定style属性：
			使用对象语法进行绑定，对象中的属性名就是设置的样式，属性值就是该样式的效果
	7.v-if v-else v-else-if：
		1.v-if：添加或删除元素，如果true添加，false删除
		2.v-else：无法单独使用，前面必须有v-if，如果v-if为false则显示v-else的内容，反之不显示v-else的内容
		3.v-else-if：也需要配合v-if进行使用，在需要多重条件时用该指令
	8.v-show：控制元素的显示与隐藏，使用的是css的display属性来控制
		* v-show与v-if的区别：
			1.原理：v-if是元素的添加和删除而v-show是display的显示与隐藏
			2.性能：v-if有更高的切换消耗，而v-show有更高的初始渲染消耗
			3.使用场景：v-if适合不需要频繁切换的场景，而v-show适合频繁切换的场景
	9.v-for：列表渲染 v-for="(item,index) in 数据"、v-for="(item,index) of 数据"
		* 数据类型：Array、Object、String、Number(自然数，表示数组的长度)、
		* diff算法：
			* key值的作用：在节点中如果为节点绑定了一个key值，那么这个key值会为这个节点绑定唯一的id标识，这也是diff算法的一种优化，可以根据key值更准确更快速的找到对应的节点
			减少dom的操作，优化页面的性能
			* 如果不使用key值：Vue采用的是就地复地原则，最小化的element移动，并且尝试最大程度在适当的地方对element节点做patch和reuse操作
			* 使用key值：Vue采用根据keys的顺序记录element，曾经拥有key的element如果不在出现的话，会直接remove或者destoryed
		*虚拟DOM(vnode)：
			*通过js创建一个object对象来模拟真实DOM结构，这个对象包含标签名（tab）、属性（attrs）、和子元素对象（children），通过vue中的render()函数把虚拟DOM编译成真实
			DOM，再通过appendchildren()添加到页面中
			*为什么要使用虚拟DOM：vue中虚拟DOM最大的优势就是diff算法，减少JavaScript操作真实DOM带来的性能消耗
	10.v-on：绑定事件 可以简写成 @，在vue中方法可以在data中定义，但是data的主要作用就是保存数据，方法并不是数据，所以在结构上我们不推荐将方法放入data中定义，而在vue中有专门提供
		定义方法的位置，就是methods，
		绑定一个函数时，函数如果不加括号，则会默认将$event作为参数传递，函数如果加了括号，则$event不会默认传递，需要手动给一个$event参数
		当我们需要传递除了event以外的参数时，就需要加括号来传递，反之我们一般可以不加括号
		v-on中的修饰符：
			1：.stop:表示阻止事件流
			2：.proevent:表示阻止默认事件
			3：.native:表示监听组件根元素的原生事件
			4：.once:表示当前事件触发一次后就会解除
			5：.数字:表示键盘事件的键盘码
	11.v-model：表单双向数据绑定，常见是在表单标签中出现；
		v-model原理：通过v-bind绑定输入框的value值实现数据改变输入框内容跟着改变，再通过v-on监听输入框的input事件，在事件函数中获取输入框的value值来改变数据，从而达到双向绑定的实现，v-model就是这种实现的语法糖
		修饰符:.lazy:将实时同步的input事件更改为失去焦点的change事件
					.number将输入的内容转为number类型
					.trim:自动过滤
	12.v-slot：
### vue自定义指令
* 1.全局自定义：可以在任意一个组件内使用，在main.js中定义
```js
Vue.directive('focus',{
  inserted:function(el){
    el.focus()
  }
})
```
* 2.组件内自定义：只能在当前内组件内使用,在组件实例对象中通过directives属性来创建自定义指令
```js
  directives:{//局部创建自定义指令
    'moves':{
      inserted:function(el){
        
      }
    }
  }
```
* 自定义指令的钩子函数
* 1.inserted:被绑定的元素插入父节点时调用,俩参数
* 2.bind:只调用一次，指令第一次绑定到元素时调用，可以在这里做一些初始化的工作
* 3.update:所在组件的VNode更新时调用，有可能在子组件的VNode更新前调用
* 4.componentUpdate:指令所在的组件及子组件的所有VNode全部更新完之后调用
* 5.unbind:只调用一次，指令与元素解绑时调用
* 在自定义指令的钩子函数中每个函数都有两个参数，分别为el、binding，el接收到的时当前指令绑定的DOM元素，binding接收到的是一个对象：1.name：自定义指令名、2.rawName：带v-前缀的自定义指令名、3.value：自定义指令的值、4.oldValue：当前指令绑定的改变前的值、5.expression：以字符串形式记录指令的值
* 在以上属性中所有的属性都是只读属性，不允许修改
### Vue中的配置项：
	1.el:用于将Vue实例挂载到某一个dom元素节点 值可以是一个字符串也可以是一个element元素，如果是字符串，则需要以css选择器的形式来选择对应的元素，如果是element，那么必须是一个元素
	，不能是元素的集合；
	为了确保选中的标签具有唯一性，通常情况下我们都是用id属性来挂载元素
	可以通过app.$el来访问Vue实例挂载的元素
	el不允许挂载到html标签和body标签上，因为这样会破坏HTML的主体结构

	2.data:用于保存Vue实例所用到的所有数据
	可以是一个对象、函数（组件中只能是函数）
	如果是函数形式，南无需要在函数中return出一个对象，该对象保存的就是Vue实例用到的数据

	3.methods:保存所有Vue实例用到的方法
	在methods中，函数不能写箭头函数，因为箭头函数this指向会发生变化无法指向当前Vue实例

	4.computed:4. 计算属性 
	* 在计算属性中书写的也是一个个方法，与methods中的内容类似，但是计算属性中的方法一般都需要给一个return返回值
	* 在页面中使用计算属性中的方法时，Vue会将计算属性中的方法作为Vue实例的属性来渲染，也就意味着页面上我们只需要使用方法名就可以渲染数据，不需要加括号调用
	* 在多次使用计算属性中的同一个方法时，Vue会将该属性值做一个缓存处理，重复使用会从缓存中读取，不会重新调用函数，也就是多次使用只触发一次函数调用，这样可以大大减少页面渲染的执行消耗
	* filters : 过滤器  特定格式转换器
	* watch：监听所有数据的变化，也是以函数的形式进行书写，函数名就是要监听的数据，函数可以接受两个参数，第一个参数是改变之后的值，第二个是原数据
	watch中监听数据的变化也可以写成对象语法：person:{			handler:可以监听数据变化；deep：当值为true，表示对数据深度监听
						handler:function(){},
						deep:true
					}
### Vue的生命周期：
	变量的生命周期：页面打开时诞生，页面关闭时销毁；局部变量函数调用时诞生，调用完销毁；闭包函数变量在调用时诞生，页面关闭后销毁；
	四大阶段：
		初始化：
		挂载：
		更新：
		销毁：
	八个生命周期函数：
		
### methods和computed两者有什么异同？
* 共同点： 两者内部书写的都是方法
* 不同点： 
  * 1. computed有缓存，多次调用只执行一次，而methods中没有缓存，多次调用会执行多次
  * 2. computed在页面中使用时不需要加括号，methods使用时需要加括号
### vue中各个属性的默认加载顺序：
	在vue的源码中的initState函数中提供了加载顺序
	props---methods---data---computed---watch
	在以上属性中定义的任何名字不建议出现相同（watch除外）
### v-text、v-html、插值表达式三者的区别：
	v-html可以解析html代码，但v-text和插值表达式不能解析
	插值表达式不会替换标签原有内容，而v-html和v-text会替换原有的内容
### Vue的组件化（重要*****）
* 什么是组件化
   当处理一件复杂的事情时，我们可以将这个事情拆分成若干个小事情，将这些小事情一一解决之后，实际上大的问题也就迎刃而解，这种处理事情的思想，实际上就是组件化思想
* 组件化的优点
  便于后期的管理和维护，有利于代码的复用，减少页面的代码量

### 使用组件的步骤
1. 调用 Vue.extend()  
    调用这个方法创建一个组件的构造器
    在调用时需要传递一个对象类型的参数
    这个对象中的属性和Vue实例中的属性几乎一样，但是需要一个temptale属性用于自定义组件的模板，也就是HTML内容
2. 调用 Vue.component()
    这个方法是将组件注册成一个全局组件，里面有两个参数，第一个参数是组件使用时的标签名，第二个参数是要注册的组件
3. 在Vue实例所挂载的HTML标签内使用注册好的组件就可以

#### 在组件的template模板中，必须存在一个root element 也就是根元素，所有的组件内容要写在根元素内部


####  webpack的基本使用
* 定义： 是一个现代化的javascript应用的静态模块的打包工具

* 安装命令：
  npm i webpack webpack-cli -g 
* 查看是否安装成功：
  webpack -v

###  npm安装
* npm是一个包管理工具 npm是node安装时自带依赖安装的内容
* npm install 要安装的程序
* npm i 要安装的程序
* -g  表示全局安装  
* --save 表示在本地安装并且将安装的程序描述加入到package.json文件中

* npm uninstall 程序名  可以卸载对应的程序

* 全局安装和本地安装：
  全局安装就是指在电脑的任意一个磁盘的任意位置都可以访问对应的程序
  本地安装就是指只能在安装该程序对应的文件夹内访问

### 工程化项目的搭建
* src目录 ： 主要是存放所有当前项目的代码
* dist目录 ： 主要是存放打包之后生成的代码
* public目录 ： 主要是存放一些项目需要的静态资源文件
* webpack.config.js文件 ： 主要作用是关于webpack的配置文件


###  webpack打包命令
webpack 原文件 -o 打包后文件目录
webpack ./src/index.js -o ./dist/js


####  cmd常见命令
*  cd..  表示返回上一级目录
*  cd 目录名 表示进入当前目录的子目录

### 项目的初始化配置：
* 生成配置文件：npm init  生成一个package.json文件
* 本地安装一个webpack3.9.0版本，npm i webpack@3.6.0
* 执行webpack命令时，发现永远执行的都是全局的webpack，不会执行本地
* 如果要执行本地webpack，要在package.json中的scripts中配置相关的命令来执行:"build":"webpack",之后可以通过npm run build 命令运行本地webpack，如果没有webpack则会进行全局webpack
### webpack中loader使用：
* 1.下载loader
* 2.配置loader的规则

### 打包css文件
```
下载安装对应的css-loader：npm i css-loader --save-dev
```
* --save-dev：表示只在开发阶段需要以来的内容，真正发布之后则不再需要
	
### 创建项目
### project目录
* src目录
   * main.js
   * App.vue
* pubilc目录
* webpack.config.js
* index.html
### 初始化项目
```
npm init -y
```
### 安装本地webpack
```
npm i webpack webpack-cli
```
### 配置webpack
```
const path=require("path")
module.exports={
    mode:"development",
    entry:"./src/main.js",
    output:{
        path:path.resolve(__dirname,"dist"),
        filename:"index.js"
    }
}
```
### 添加本地运行命令
* 在package.json文件中添加以下配置
```
"scripts": {
    "build":"webpack"
  },
```
### 通过npm安装Vue
```node
npm i vue@2
```
### 在src目录下的main.js中引入vue
```js
import Vue from "vue"
```
* 这样引入我们发现后面的“vue”没有加任何的路径标识，当我们直接写一个名字时，webpack会自动从node_module目录内去查找对应的文件，如果找到的是一个文件夹，
* 那么webpack会自动从该文件夹查找index.js进行编译加载
### 在src目录下的main.js中创建vue实例
```js
let app=new Vue({
el:'#app',
data:{

}
})
```
### 在index.html中可以写html代码

### 通过打包npm run build 对项目打包
### 在vue最终发布的时候，会构建出两种版本
* 1.runtime-only
  * 代码中是不允许有任何的template，也不会去直接编译这个模板，需要用到render函数去渲染
* 2.runtime-compiler
  * 代码中可以编译template
### 打包后发现页面报错我们需要切换vue版本
*在webpack.config.js中配置
```js
    resolve:{
        alias:{
            "vue$":"vue/dist/vue.esm.js"
        }
    }
```
### vue是一个SPA框架（单页面富应用）
一个网站只存在一个html文件，其他的页面都是通过路由或者其他方式跳转的
### el和template两者的关系
* el是将vue实例挂载到某个已经存在的html元素上
* template是将vue渲染到某一个模板中
* 如果在一个vue实例中既有el又有template，那么vue实例首先先挂载el所对应的html元素，再用template中的模板内容替换el所挂载的元素
### 创建一个独立的.vue文件
### 当npm run build 打包时出错，无法打包.vue类型的文件，需要安装对应的loader
* npm i vue-loader@15.0.0
* npm i vue-template-compiler 
### 如何打包html文件 需要安装Plugin
* 1.下载:HtmlWebpackPlugin：npm i html-webpack-plugin --save-dev
* 2.引入
```
const HtmlWebpackPlugin=require("html-webpack-plugin")
```
* 3.配置
```
plugins: [
	    new VueLoaderPlugin(),
        new HtmlWebpackPlugin({
            template:"index.html"
        })
    ]
```
### 本地服务器 webpack的热更新
* 1.下载：npm i --save-dev webpack-dev-server
* 2.配置：
```    
devServer:{
	contentBase:"./dist",
	inline:true
}
```
* 3.添加命令
在package.json的scripts中添加
```
"server":"webpack-dev-serve"
```
* 4.使用命令运行服务器
  npm run serve
* 5.通过 http://localhost:8080/ 可以访问当前项目内容
### 安装 vue-cli 脚手架
### vue-cli 搭建项目
* 创建项目：vue create 项目名
* please pick a preset：请选择想要的预设置
* 	Manually select features：表示自己想要的内容
* 	Babel：转换器，用于将ES6转为ES5
* 	TypeScript：项目是否支持TS语言
* 	Progressive Web App (PWA) Support：是否该项目要作为App使用Router：路由，是否使用vue-router
* 	Vuex：是否使用Vuex
* 	CSS Pre-processors：是否使用css预编译语言
* 	Linter / Formatter：是否使用esLint检测工具来规范格式化代码
* 	Unit Testing：单元测试
* 	E2E Testing：end to end，端对端测试
* 	? Please pick a preset: Manually select features
* 	? Check the features needed for your project: Babel, Linter
* 	? Choose a version of Vue.js that you want to start the project with(选择一个vue.js的版本):2.x
* 	? Pick a linter / formatter config: Standard
* 	? Pick additional lint features: Lint on save
* 	? Where do you prefer placing config for Babel, ESLint, etc.? :In dedicated config files
* 	? Save this as a preset for future projects? (y/N) n
* 运行项目：npm run serve
### 如何关闭esLint代码检测
1.在项目中 vue.config.js文件中
如果更改了vue.config.js，那么我们的项目必须要重新启动才能生效
```js
module.exports = defineConfig({
  lintOnSave:false
})
```
### src目录下的assets目录
* 该目录和public目录相似，主要放当前项目的静态资源
### components目录
* 存放组件
### views目录
* 存放页面级组件
### network目录
* 存放一些网络请求的封装
### router目录
* 存放vue路由信息
### store目录
* 存放vuex状态管理信息
### utils
* 存放一些常用的工具类函数
### 所有的.vue文件 首字母一般为大写
* 创建组件：新建一个.vue文件
* 引入文件：通过import引入
* 挂载组件：components中挂载
* 使用组件：template模板中使用
### 组件之间的通信（重要）
* 父子组件的通信
  * App.vue
	* Home.vue
	* aaa.vue
* 组件作用域
 * 每一个组件内部的数据或者方法只能被当前组件访问，其他组件无法访问，组件与组件之间时互不影响的
### 父传子数据
* 1.在父组件的子组件标签上自定义一个属性，属性值就是子组件传递的数据
* 2.在子组件内通过props属性来接受父组件传递的数据
* 3.在子组件内就可以使用传递的数据
### props属性的使用
* 1.props可以是一个数组，每一个数组项就是负组件中子组件标签自定义的属性名，这样可以通过名字来获取对应的数据
* 2.props可以是一个对象，每一个对象属性名就是父组件中的自定义属性名,属性值是该数据的数据类型
* 3.props可以是一个对象，属性值可以是一个对象，该对象包含两个属性：type和default，唐渝鹏表示数据类型，default表示数据的默认值
```js
props:{
  mes:{
    type:String,
    default:"按钮"
  },
  list:Array
},
```
* 组件名不能使用HTML中原有的标签名
#### 子传父数据
* 前提：子组件中必须要触发一个事件函数或者生命周期函数
* 1.在子组件的事件函数中，通过this.$emit()方法，向父组件发出一个自定义事件，同时携带数据
* 2.在父组件的子组件标签上通过v-on监听子组件发出的自定义事件，绑定一个事件触发函数
* 3.在父组件的事件触发后可以接收到一个参数，该参数就是子组件传递过来的数据
#### 组件中的data为什么必须是一个函数？
* 1.项目中根组件中的data可以是函数也可以是对象，因为每一个项目的根组件有且只有一个
* 2.项目中除了根组件以外的其他组件data只能是函数，不能是对象，原因是组件具有可复用性，一旦使用对象类型，多个组件复用时会造成数据共享，不利用数据的复用，而写成函数后每一次复用组件都会生成一个全新的data对象，这样组件之间的数据不会相互影响
#### 非父子组件之间的通信
* 1.新建一个bus.js文件，该文件需要导出一个空的vue实例
* 2.将bus.js引入到main.js中，并将bus.js空实例挂载到Vue的原型对象中
* 3.需要传出数据的组件中使用this.$bus.$emit()来发出自定义事件并传值
* 4.在需要接受数据的组件中使用this.$bus.$on()来监听自定义事件并接受值
### 安装yarn包工具
* npm i yarn -g
### 组件传值（什么是单向数据流）
* 1.如果是基本数据类型父组件向子组件传值采用的是单向数据流，父组件数据发生改变会影响子组件，子组件修改数据无法影响父组件，这个数据是一个基本类型的数据
* 2.如果是引用数据类型，那么父子组件之间传递的是数据的地址，相互修改都会发生影响
### 如何让css只在当前组件生效
* 在组件的style标签上添加一个scoped属性，该属性表示启用样式作用域，当我们添加了这个属性后，style的样式就只对当前组件有效，不会影响其他组件
### vue项目如何配置全局样式
* 1.在App.vue的style中使用@import来导入一个css文件
* 2.在main.js中使用import来导入一个css文件（常用）
### css预编译语言
* less
 * 1.嵌套语法
  ``` css
  .head{
		.nav{
			width: 300px;
			height: 300px;
			background-color:pink;
		}
	}
  ```
 * 2.变量：必须以@开头，结尾必须有分号
 ```css
 @color:#a8597c;
	.head{
		.nav{
			width: 300px;
			height: 300px;
			background-color:@color;
		}
	}
 ```
 * 3.混合（Mixins）
 ```css
  .base{
		width: 200px;
		height: 200px;
		border:1px solid red;
		border-radius: 10px;
	}
	.fl{
		float: left;
	}
	.a{
		background-color:pink;
		.base();
		.fl()
	}
	.b{
		background-color:purple;
		.base();
		.fl()
	}
 ```
* scss/sass
### 插槽的使用
* 作用是在父组件中向子组件中传递定制化的内容
### 插槽的分类
* 匿名插槽：没有名字的插槽
  * 使用场景： 当组件中只有一个位置需要定制化时，那么可以使用匿名插槽
* 具名插槽：具有name属性的插槽  
  * 使用场景： 当组件中需要使用多个插槽时，那么需要使用具名插槽
	```html
	<slot name="a"></slot>
	<div slot="a"></div>
	```
* 作用域插槽：HTML结构由父组件来决定，但是数据是子组件提供
  * 子组件：
	```html
	<slot name="s" :aa="list"></slot>
	```  
  * 父组件：
	```html
	<template v-slot:s="aa">
		{{aa.aa}}
	</template>
	```
* 解构插槽：也是作用域插槽
  * 子组件：
	```html
	<slot name="s" :aa="list"></slot>
	```  
  * 父组件：
	```html
	<template v-slot:s="{list}">
		{{list}}
	</template>
	```
### 前后端交互

### 项目组：
* 产品经理
* 前端开发
* 后端开发：服务器和数据库
* 测试
* 运维
### web的发展史
* 1.只有纯文字的内容，没有任何用户的交互操作，前后端不分离（后端渲染）
* 2.Ajax的出现（前后端分离阶段）
* 3.前端框架的出现（Vue、react）（前端渲染）（axios）
### ajax的使用
* 1.创建一个xml实例对象
```js
var xml=new XMLHttpRequest()
```
* 2.打开与后端的接口通道
```js
xml.open("get","https://api.it120.cc/axd/banner/list")
```
* 3.向后端发送请求
```js
xml.send()
```
* 4.监听服务器响应状态
```js
xml.onreadystatechange=function(){
  if(xml.readyState==4){
    if(xml.status>=200&&xml.status<300){
			console.log("执行成功")
      console.log(JSON.parse(xml.response));
    }
  }
}
```
### readyState状态码
* 0：ajax的初始化状态，也就是在调用open方法之前的状态
* 1：在ajax与后端建立连接到发送完请求阶段
* 2：服务器接收到前端的请求时
* 3：服务器正在处理
* 4：服务器响应完成
### status(HTTP状态码)
* 1XX:服务器正在处理中，还没有完成
* 2XX:成功，200表示没有任何问题
* 3XX:重定向，请求的资源位置发生了变化，需要重新请求301（永久重定向）、302（临时重定向）
* 4XX:客户端错误（前端错误）404
* 5XX:服务端错误
* 对接口
### 获取服务器响应的数据
* 接收到的是一个JSON字符串格式的数据，我们需要通过JSON.parse转换成JSON对象使用
```js
JSON.parse(xml.response)
```
#### ajax是一个异步编程
#### get和post请求的区别：
* 1.安全性：post相比较于get，安全性会更高一点
* 2.数据大小：get请求最大传输约2kb，post请求无上限
* 3.传输速度：get请求传输更快，post稍慢
* 4.缓存性：get可以被缓存，post无法被缓存
### get请求参数需要在url路径后面以query查询字符串形式来添加
* "https://api.it120.cc/axd/shop/goods/detail?id=1192213&token=agg123h123h123"
### post请求参数需要在send方法中以query字符串形式传递，同时我们需要设置请求头，将内容类型更改成表单提交方式
* xm.setRequestHeader("Content-Type","application/x-www-form-urlencoded")
### 协议 域名(IP地址) 端口号

### http和https两者的区别
* 1.https比http协议更安全，因为其中加入了ssl加密协议
* 2.两者使用的端口号也不一样，http使用的80端口，https使用的443端口
#### IP地址：（电脑在网上的身份标识）
* 广域网 
* 局域网 192.0.0.1
* 本地 127.0.0.1
#### 端口号（电脑上每一个应用程序的身份标识）

### 同源策略
* 协议、域名、端口号一致

### 跨域请求
* JSONP
* iframe
* cors（后端）
* proxy代理（常用）
* nginx反向代理（公司常用）
### 网络请求的框架 axios
* 是一个基于ajax及promise开发的应用于在vue中实现网络请求的框架
* 下载安装 npm i axios
* 引入：import axios from “axios”
* 使用：axios({
* //配置项
* })
### 常见的axios配置项
* url：请求的路径
* baseUrl：请求的基本路径
* method：请求的方式
* headers：请求的头设置
* parmas：url的查询对象，主要适应于get传参
* data：请求体，只要是用于post传参   
* data有两种方式：字符串、对象，如果请求类型是application/x-www-form-urlencoded这种类型，需要字符串传递，如果是application/json那么需要使用对象传递参数
* timeout：设置网络请求的超时时间
* transformRequest：转换请求数据
* transformResponse：解析请求数据
### axios二次封装使用
### axios并行请求数据
```js
created() {
    axios.all([
      axios({
        method:"get",
        url:"https://api.it120.cc/axd/banner/list"
      }),
      axios({
        method:"post",
        url:"https://api.it120.cc/axd/notice/list"
      })
    ]).then(res=>{console.log(res);})
  },
```
### axios的拦截器
* 请求拦截：主要作用将发送给服务端的内容统一做一些处理操作，比如在headers中添加身份令牌(token)等
* 响应拦截：主要作用对拿到的数据先进行一次简单处理，将处理的结果返回页面
### 网络请求的方式
* get
* post
* delete
* head
* put
* patch
#### git使用 gitee
* 设置用户名：git config --global user.name 'gitee用户名'
* 设置用户邮箱：git config --global user.email '邮箱'
* 查看配置成功：git config --list
### git常用命令
* git status：表示查看git仓库状态
* git add 文件名：表示将文件从工作区传到暂存区
* git commit 文件名 -m 描述：表示将文件从暂存区添加到仓库
* git log：表示查看git提交记录
* git reset --hard 版本号：表示恢复之前提交的某一个版本
* git reflog：表示查看所有的版本记录
### 什么是git
项目管理工具
### svn和git两个有什么区别
* svn 集中式管理
* git 分布式管理
	* 1.工作区：红色
	* 2.暂存区：绿色
	* 3.存储区（仓库）：不显示
### GIT常用命令
* git init：初始化git仓库
* git app 文件名：将文件从工作区添加到暂存区
* git app . ：将工作区所有文件一次性添加到暂存区
* git status：查看当前文件状态
* git commit -m 描述信息：将文件从暂存区添加到仓库
* git log：查看提交的历史记录（只能查看当前版本之前的记录）
* git reflog：查看所有版本记录
* git reset --hard 版本号：恢复某一个版本内容
### 多人协同开发 远程仓
* github:https://www.github.com
* gitee:https://www.gitee.com
* gitlab:https://www.gitlab.cn
* 码云：也就是gitee
### 创建SSH key
* ssh-keygen -t rsa -C '账号'：配置ssh公钥
* ssh -T git@gitee.com:查看是否可以于远程仓链接
### 本地有项目，远程仓没项目
* 1.确认将项目添加到本地仓保存
* 2.再gitee中创建一个空的远程仓库
* 3.使用以下命令和远程仓链接：git remote add origin git@gitee.com:du-jiameng/project.git 和 git push -u origin "master"
### 远程仓有项目，本地没有项目
* git clone 项目地址：git@gitee.com:du-jiameng/project.git
* 2.进入克隆下来的项目目录
* 3.在项目中使用npm i 安装需要的依赖
### 本地和远程都有项目
* 1.将本地修改过的代码提交到本地仓
* 2.使用git pull拉取远程仓最新的代码
* 3.使用git status 检查确认工作区是否还有内容
* 4.确认无误使用git pus 提交到远程仓
### 合并冲突问题
* 当git pull拉取代码时，有可能产生合并冲突问题
* 当遇到合并冲突，我们需要手动找到冲突代码的位置，来决定该位置的代码如何保留，手动删除冲突产生的无效代码
* 修改完之后重新提交到本地仓，之后git push到远程仓
### git分支操作
* 同时并行推进一个项目的多个功能时，为了提高开发效率，我们可以使用分支进行管理
* 各个分支在开发过程中，如果某一个小分支开发失败，不会对其他分支造成任何影响，只需要对该分支重新开发即可
#### 分支操作的命令
* git branch -v ：查看分支
* git branch 分支名 ：创建分支
* git checkout 已有分支名 ：进入分支
* git checkout -b 分支名 ：创建并直接进入分支
* git branch -d 分支名 ：删除一个分支；不能删除当前所在分支
* git merge 分支名 ：合并分支；如果需要b分支合并到a分支上，那么该命令需要到a分支下操作
* git merge 分支名 -m 描述 
* git tag -a 版本号 -m 描述信息 ：将当前项目做一个版本标记
* git push origin 版本号 ：将版本推送到远程仓
* 如果使用的时https方式与远程仓连接，那么在每一次操作远程仓时都需要确认身份，如果用ssh，那么必须在gitee个人中心中配置ssh公钥，配置完操作就不需要任何身份验证
### 常见的UI框架
* vant-ui(有赞--移动端)
* element-ui(饿了么--PC端)
* bootstrap(响应式)
#### vant-ui使用
* 下载安装：npm i vant@latest-v2 -S
* 在main.js中全局引入：
```js
import Vant from 'vant';
import 'vant/lib/index.css';
Vue.use(Vant);
```
















