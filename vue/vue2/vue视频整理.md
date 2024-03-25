

初始化项目  

```
vue init webpack demo1
```



### 常识：

```
vue 参数中配置项，都用单引号  ，隔开。  

表单输入11  有个天气查询api
凡是以：的，前面是属性，后面是属性值。
<school :属性='属性值'></school>
2.
main.js为什么是程序入口
因为 实例在这里啊
let vm = new Vue({
	components: {
		App
	},
	template: '<App/>'
})
Vue.use({
	vm
})

```

## vue 单页面中的配置项

```
export default {
       params:{},//组件传值时用
		data() {
			return {
				message: '1234',
			}
		},
		// 8个钩子函数
		mounted() {
			console.log(this)
		},	
		// 方法
		methods:{},
		// 计算属性
		computed: { },
			// 过滤器
		filters：{},
		 watch: {  // 监听属性 监听data中的数值变化，变化即触发
             },
		}



```



## vuex中的配置项

```

2.仓库的标准配置项；
export default new Vuex.Store({
	//相当于data
  state: {
  
  },
  //相当于 store 的计算属性
  getters:{

  },
  //相当于methods
  mutations: {
  },
  //异步方法
  actions: {
  },
  //模块
  modules: {
  }
})
```

注意误解： 数据仓库不止是data,数据，还可以是方法。

​    actions    mutations     异步方法，调用mutations， 操作state数据  存取。

之前的文章中用到过 Vuex 的 mutations，从结果上看，mutations 类似于事件，用于提交 Vuex 中的状态 state

action 和 mutations 也很类似，主要的区别在于，action 可以包含异步操作，而且可以通过 action 来提交 mutations

另外还有一个重要的区别：

mutations 有一个固有参数 state，接收的是 Vuex 中的 state 对象

action 也有一个固有参数 context，但是 **context 是 state 的父级**，包含 state、getters

https://www.cnblogs.com/wisewrong/p/6402183.html

#### vuex axios请求，存储公共数据 和组件中使用方法

```
import Vue from 'vue'; // 首先引入 vue
import Vuex from 'vuex'; // 引入 vuex
import API from '../API/index' // 这里是因为封装了 axios 的方法在里面, 所以可以直接引用
Vue.use(Vuex)
export default new Vuex.Store({
  state: {
    domainList: []
  },
  mutations:{
    updateDomain (state, payload) {
      state.domainList = payload
    }
  },
  actions:{
    getAllDomain (context) {
      API.getStatList(true).then((response) => {
        let res = response.data;
        if (res.code == 0) {
          context.commit('updateDomain', res.data.items);
        }
      })
    }
  }
})

组件中
1. 执行方法
2. 拿数据
export default {
  computed: {
    domainList () {
      return this.$store.state.domainList; // 获取 state 中的 domainList
    }
  },
  mounted () {
    this.$store.dispatch('getAllDomain'); // 直接调用 store/index.JS 中的方法
  }
}
```

### vuex中mutations一个方法需要调用另外一个方法

在vuex中的mutations方法，想调用mutations中的另外一方法，还是用commit,只需要使用this.commit('function')，当前的this指向的就是当前模块中的mutations；

注意

vuex中mutations 不能return 

## [vue-cli中的build.js配置文件详细解析](https://www.cnblogs.com/wulinzi/p/8066236.html)

这是vue-cli脚手架工具的生产环境配置入口 package.json中的"build": "node build/build.js"的直接指向。

打包的配置项。

## vue 中的config文件

用vue-cli 自动构建的目录里面  （环境变量及其基本变量的配置）  处理开发环境和上线的环境，关于路径的处理。

私有样式：

<style scoped>

 <style>
## [Vue 组件 data为什么是函数？](https://www.cnblogs.com/libin-1/p/6878057.html)

在创建或注册模板的时候，传入一个data属性作为用来绑定的数据。但是在组件中，data必须是一个函数，而不能直接把一个对象赋值给它。

```
var component1 = new MyComponent()
var component2 = new MyComponent()
// 上面实例化出来两个组件实例，也就是通过<my-component>调用，创建的两个实例

component1.data.a === component2.data.a // true
component1.data.b = 5
component2.data.b // 5
```

可以看到上面代码中最后三句，这就比较坑爹了，如果两个实例同时引用一个对象，那么当你修改其中一个属性的时候，另外一个实例也会跟着改。这怎么可以，两个实例应该有自己各自的域才对。所以，需要通过下面方法来进行处理：

```
var MyComponent = function() {
  this.data = this.data()
}
MyComponent.prototype.data = function() {
  return {
    a: 1,
    b: 2,
  }
}
```

这样每一个实例的data属性都是独立的，不会相互影响了。所以，你现在知道为什么vue组件的data必须是函数了吧。这都是因为js本身的特性带来的，跟vue本身设计无关。其实vue不应该把这个方法名取为data()，应该叫setData或其他更容易立即的方法名。

## 关于vue的热加载编译

vue没有热加载编译
可能原因：

1.  vue 监控文文件 触发 是保存事件。 保存后发现有代码改变就进行重新编译。 因为浏览器只能解析显示编译后的 js css html。

   并不是直接读取vue组件。  但是编译的越频繁，消耗性能越多。 所以，热加载监控文件区域只是 src。 故，main.js pro.js等配置文件修改，并不会触发重新编译。

2.  修改src内的组件，编译失效。  可以npm install 。因为编译本省也是一段js 。 或者是插件，有损坏或者报错的可能。初始化一下。

目前碰到的所以的编译失效，都是这两种情况。   记录一下


## v-text  v-html

````javascript
<template>
  <div id="ceshi">
    <h1>测试文本</h1>

    <span v-text="msg"></span>

    <span v-html="html"></span> //如果data值是html标签，可以用v-html，可以解析标签。
  </div>
</template>

<script>

export default {
  name: "App",
  data() {
    return {
      msg: "我是文本",
      html:"<h1>我是标签</h1>"
    };
  },
};

</script>
总结： v-text  是属性绑定，绑定对象标签内整体替换，所以里面的旧数据会被替换。
      v- html 作用和text相似，但是可以解析标签。

````





# 第一天

## [ v-bind 详解](https://www.cnblogs.com/shix0909/p/11188263.html)

v-bind指令用于给html标签设置属性。

总结： v-bind ： 属性名字='  对前面进行判断 '      判断区域可以是变量 ，布尔值，函数，对象，数组。 总之：vue规则获取之后会进行计算。

```
<!-- 完整语法 -->
<a v-bind:href="url"></a>

<!-- 缩写 -->
<a :href="url"></a>

```

## v-bind入门

```
<div id="app">
  <div v-bind:id="id1">文字</div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    id1: 'myid'
  }
})
</script>
```

会渲染如下：

```
<div id="myid">文字</div>
```

## 字符串拼接

```
<span :text=' "we" + 1 '>使用</span>
```

会渲染如下：

```
<span text='we1'>使用</span>
```

## 运算：

```
<div :text='1 + 2'>test</div>
```

会渲染如下：

```
<div text="3">test</div>
```

## 调用函数：

```
<div :text='getText()'>test</div>
 ......
 <script>
export default {
  methods: {
    getText() {
      return "this is text"
    }
  }
}
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

渲染成：

```
<div text="this is text">test</div>
```

## 使用对象：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<template>
  <div class="hello">
    <div :text='obj'>test</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      obj: Object()
    }
  }
}
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

结果：

```
<div text="[object Object]">test</div>
```

如果对象有toString方法：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<template>
  <div class="hello">
    <div :text='obj'>test</div>
  </div>
</template>

<script>
var obj = Object()
obj.toString = function(){
  return "data in obj"
}
export default {
  name: 'HelloWorld',
  data () {
    return {
      obj: obj
    }
  }
}
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

则渲染的是toString方法的值：

```
<div text="data in obj">test</div>
```

## 和数组使用：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<template>
  <div class="hello">
    <div :text='array'>test</div>
  </div>
</template>

<script>
var array = Array()
array[0] = "1"
array[1] = "2"
export default {
  name: 'HelloWorld',
  data () {
    return {
      array: array
    }
  }
}
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

渲染为：

```
<div text="1,2">test</div>
```

## v-bind vs 计算属性

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<template>
  <div class="hello">
    <div :text='myText'>test</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      value: "data"
    }
  },
  computed: {
    myText: function(){
      return "value is " + this.value
    }
  }
}
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

稍微对比一下，我们不难发现，计算属性和上面的各种功能是一样的，但是在字符串拼接的情况下，使用计算属性的好处是分离了，不在html中写逻辑。所以计算属性是更推荐的用法。

## class 属性绑定

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="app">
  <div v-bind:class="{active: isActive}">文字</div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    isActive: true
  }
})
</script>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

如果同时多个类都要判断，则可写成`<div v-bind:class="{active: isActive, highlight: isHighlight}">文字</div>`。

## 绑定computed属性：

而且还可以绑定computed里的属性，毕竟data的数据是静态的，computed的属性可以计算：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<div id="app">
  <div v-bind:class="classObject">文字</div>
</div>

<script>
new Vue({
  el: '#app',
  computed: {
    classObject: function () {
      // 计算过程省略，假设得出了isActive和isDanger的布尔值
      return {
        'active': isActive,
        'text-danger': isDanger
      }
    }
  }
})
</script>
```

## 1.mvc模式

Model 模型  数据存储

view 视图层 就是可见的界面

c control  控制器  监听事件 点击事件

vue 的核心  数据驱动视图      这是一个设计思想   即 我们只需要点击事件修改数据data,界面自动改变。

定位：  中小型项目 

## 2.框架与库

框架是一套完整的解决方案   vue   angular.js react.js

库 只提供一个小功能   jq 

## 3.vue 的虚拟dom

传统的开发是利用jq 操作DOM,非常消耗资源。

现在  在js内存里构建类似于dom的对象，去拼接数据，然后把数据整体解析，一次性插入到html里去。 这就形成了虚拟dom.

vue1.0没有虚拟dom。2.0改成了基于虚拟dom。

4 angular 不受欢迎的原因

是他没更新一般，相当于新建一个新框架。

目前vue 和 react 较为受欢迎

## 4.vue的实质

一个封装的对象  集合了多种方法 使用者以配置项的方法进行使用

## 5.关于渲染

 {{ message }}  dom里面直接放置这个，在刷新的瞬间可以看到{}。 

	<div id="app">
		  {{ message }}
	</div>
	
	var app = new Vue({
			  el: '#app',  //确定vue生效的范围
			  data: {
			    message: 'Hello Vue11111!'
			  }
	})

## 	6. 条件渲染  /条件显示 if else

​	


	<p v-show="num==1">1111</p>
	
	<p v-else="num==3" >3333</p>
	两个后面都可以加表达式    =‘’  里面最后的结果只要是true false都可以
	
	注意： 条件渲染和列表渲染不要同时使用，因为每次渲染都要判断，降低了性能。


###  6.1 条件渲染 案例2  

````javascrpt
<template>
  <div id="ceshi">
    <h1>测试文本</h1>
<div>
    <p v-if="isvip">是</p>
    <p v-else>他不是</p>
</div>

  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      isvip:false
    }
  }
};
</script>


````

总结： 可以通过一个值，控制显示，判断显示



## 7.列表渲染 v-for

```
7.1         <li v-for="item ,key in items" :value="key">
		    {{item.message}}
			 {{item.src}}
		  </li>
		  
		  :value="key" 作用是保持唯一性。 为提升性能，vue代码在你切换时会对比切换对象，如果相同则只改       局部。  导致如登陆和注册页的输入内容不变现象。
		 详见文档：  key 管理可复用的元素
		 :value="key"   加：是绑定一个动态值。
7.2	  <li v-for="key ,keymy in items" :value="key">
		    {{key.message}}
			 {{keymy}}
		  </li>    //item  key命名不是唯一，可以随便取名。
 7.3
	  <li v-for="item ,key in items" :value="key" v-if='key%2==0'>    当循环中有判断是，先循环再判断隐藏
 7.4
 <li v-for="item ,key in items[0]" :value="key">
 当key in items[0]，选择第一个时， 会渲染出items 内所有的键值。
                  items: [
				      { message: 'Foo',name:'tom',age:10},
				      { message: 'Bar' }
				    ]
				    打印：message   name  age
```







# 第二天5.21  

## 1.模板插值 

```
1.1 
数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：
<span>Message: {{ msg }}</span>
msg 有变化，页面也会更新
1.2
<span v-once>这个将不会改变: {{ msg }}</span>  //v-once  控制标签只渲染一次， 数据再变，不发生变化。

1.3原始 HTML
双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用 v-html 指令：
  html:  <span v-html="rawHtml"></span>
data:    rawHtml:'<h1 v-html >我是h1标签</h1>',
    span 内渲染 h1标签
注意：
a 注意，你不能使用 v-html 来复合局部模板
b.你的站点上动态渲染的任意 HTML 可能会非常危险，因为它很容易导致 XSS 攻击。请只对可信内容使用 HTML 插值，绝不要对用户提供的内容使用插值。   XSS 攻击在返回数据时 植入script js 代码，修改网站到假网址上。
```

### 1.1   标签简写

```
 v-bind  是绑定数据标识
 可以简写
<a v-bind:href="url">
<a :href="url">
```

### 1.2 {{  简单的表达式使用  }} 

```
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>

有个限制就是，每个绑定都只能包含单个表达式，所以下面的例子都不会生效。
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}

注意： 逻辑多的不要用这种形式。  用vue的计算属性方法，效率更高。
```

## 2. 点击事件简写

```
<button type="button" v-on:click="chenge">修改msg值</button>
简写形式
v-on:click="chenge"
@click="chenge"


2.  点击事件后面可以加简单的表达式
           <button v-on:click="show = !show">
		    Toggle
		  </button>


     data: {
		    show: true
		  }
		  
		  
```

点击事件

````javascript
 <h1 v-on:click="fn">{{ msg }}</h1>	  
	 
	 

  methods:{
  fn(){alert(0)}

  }
````





## 3.计算属性 computed   已成功验证

```
设计目的： 想插值表达式这种，每次插值都需要计算，不管结果是否改变。  为提高效率，将结果计算一次，存起来使用。所以，对于任何复杂逻辑，你都应当使用计算属性。
{{ firstname + lastname }}

配置参数：computed：{   }    //此种方式体现在重复渲染的环境下，只改变一次，体现不出他的用处，经常性的变化的情景。

使用时按照data的数据方式{{}}插值使用即可。计算属性的值，结果值和data的值一样会挂载到vue实例下面。

      data: {
				msg: 'vue'
			}, 
			
			computed: {
				reversmsg: { //reversmsg 直接在插值中使用
					get: function() {	
                    				console.log(0)//  正常来说，计算属性的内容 加载自动执行。
							return this.msg.split('').reverse().join('')
					},
					set: function(newValue) {//reversmsg  计算的值变化后，触发set函数
							console.log("newValue")
					} 
				}

			}

补充：
关于 return 函数
  var x=20;
		function fn(){
			var totle=x*2;
			return totle
			
		}
		
		console.log(fn())
打印fn()，得出结果；打印fn，只是打印出函数，没有结果，因为没有执行。
```

### 计算属性的set get

````javascript
<template>
  <div id="ceshi">
    <h1>测试文本</h1>

    <span >fullName -- {{ fullName }}</span> <br>
    <span >fullName -- {{ fullName }}</span> <br>
    <span >fullName -- {{ fullName }}</span> <br>
    <span >fullName1 -- {{ fullName1 }}</span> <br>

    <input type="text" v-model="fullName">

  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      msg: "我是文本",
      firstName: "l",
      lastName :"yx",
    }
  },

computed:{
  fullName1(){   //计算属性一般只使用 get 获取原始数据处理后的值。
      return this.firstName + " "+ this.lastName
  },

    fullName:{//fullName是一个计算属性
                    get() {//当取这个属性值的时候get方法会被执行
                    console.log("生效了");

						return this.firstName +" " +this.lastName;
                    }
                    ,
                    set(value) {//当设置fullName 这个生成的值的时候set方法会被执行
                    console.log(value);
				 this.firstName = "set生效"
					}
				}
}
 
};
</script>
````

总结：为什么要用计算属性，因为 页面多次使用 这个计算后的值， 第一次计算会进入到缓存中，性能消耗较少。





## 4.侦听属性 ： watch 方法

```
作用：它数据变动而变动时，触发事件
配置项关键字段：

data:{
	msg:'vue'},
}

watch:{
			msg:function(vale){
				console.log(vale)
			}
		}
msg 数据被修改后，触发该watch方法。

监听 不要滥用，影响性能。


  watch:{
        msg:function(newd_ata, old){   // 接受两个值，一个是改变前，一个改变后
               console.log(newd_ata , old)
        }
  }
```





## 5.Class 与 Style 绑定 5种方式

```
<div v-bind:class="{ active: isActive }"></div>
简写   :class="{ active: isActive }"

             active: isActive   active是一个对象，前面是属性，后面是布尔值控制
            <div :class="{active:istrue}" class="box">istrue</div>
			<div :class="styleobj1">styleobj1 数组形式</div>
			<div :class="zifuchuan">styleobj1 字符串</div>
			
			
				data:{
				istrue:true,// 对象方式
				styleobj:{active:true, 'col-lg-6':true}, //直接放置对象
				styleobj1:["active" ,'col-lg-6'],//放置数组
				zifuchuan:"aa bb cc",//放置字符串
				max:['acb',{active:true}]//混合形式
			}		
			
			
			
			
```

## 6 css 的内联样式

```
css 样式写在标签内
<div class="box" style="background-color: red;height: 200px;width: 200px;"></div>
语法：  v-bind:style
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>


详见官方文档

```

## 7.事件处理

### 7.1监听事件

```js
7.1  表达式
	<button v-on:click="counter += 1">Add 1</button>
			{{ counter }}
                data: {
				counter: 0
			  }

7.2事件处理方法
点击可以利用的值
		<ul>
			<li v-for="item ,index in stars" @click="clickEvent(item,index,$event)">                        {{item}}---- {{index}}   </li>
		</ul>


        methods:{
				clickEvent:function(item,index,$event){
					console.log($event)
				}
			}


注意： vue 归根到底是一个构造函数， 
app.clickEvent()    在js中 故也可以调用。
```

### 7.2 事件修饰符

```
<a v-on:click.stop="doThis"></a>
点击子盒子， 不向外扩展。

	<form action="" method="post">
		<input type="text" placeholder="普通输入框">
		<input @click.prevent="fn"  type="submit" value="提交"/>
	</form>
.prevent//阻止默认事件

修饰符是以点开头的特殊后缀，表明指令需要以一些特殊的方式被绑定。例如 .prevent 修饰符会告知 v-on 指令对触发的事件调用 event.preventDefault()：





```

### 7.3 vue中的事件

```
1.
vue中输入框事件的使用——@input、@keyup.enter、@change、@blur



```





## 8.表单输入绑定

```
文本
<input v-model="message" placeholder="edit me">
多行文本
<textarea v-model="message" placeholder="add multiple lines"></textarea>
     ！在文本区域插值 (<textarea>{{text}}</textarea>) 并不会生效，应用 v-model 来代替。

复选框

<input type="checkbox" id="checkbox" v-model="checked"> checked
<label for="checkbox">{{ checked }}</label>
    <input type="checkbox" id="checkbox" v-model="checked">
    checked 的值是true 或者 false 

3.
			<span v-for="item ,key in fruite">

				<input type="checkbox" v-model="checkedfruits" :value="item">
				{{item}}
			 </span>
			 你选择的水果是：{{checkedfruits}}
由于input是单标签， 所以循环时 加span标签协助

4. 单选框   input  type=radio

复选框  输出的是个数组， 单选框输出是一个值。

5.下拉框
<select v-model="checkmycity">
	<option value="">请选择</option>   //加上一个空的
	<option :value="item" v-for="item ,key in city"> {{item}}</option>
</select>



              city: ['北京', "深圳","郑州"],
				checkmycity:'北京' //默认选中

		！:value="item" 注意冒号，动态绑定
		
修饰符

lazy    事件转为为失去焦点 chenge执行
number   转化数字
.trim  去首位空格
可以堆叠使用

<input v-model.lazy.trim="msg">


```

# 第三天

## 1 .组件过渡 css

```
 作者设计：
 <transition name="fade">   //transition 标签  加name名字  v-if
    <p v-if="show">hello</p>
  </transition>

核心点就是：  加入标签transition  和name, 然后vue会 控制class切换， 样式自己写。
另外： class可以自定义   便于使用animated 插件等


自定义：  关键点：1.引入正确的css   2.默认class名的转换
			  <transition
			    name="custom-classes-transition"
			    enter-active-class="animated bounceInUp"
			    leave-active-class="animated slideOutRight"
			  >
			    <p v-if="show" class="box">hello</p>
			  </transition>

```

## 2.todolist

```




```

## 3. 8个钩子函数

### 生命周期函数

```
  beforeCreate    此时data和方法还没绑定到app实例对象上
   Create       已绑定
   
 beforeMount  根据数据渲染的dom对象  拿不到
 mounted         可以拿到
 
 beforeMount: function() {
				console.log("beforeMount")    
			},
			mounted: function() {
				console.log("mounted")
				let dom= document.querySelector('.redbg')
				console.log(dom)	
			},
beforeUpdate	页面数据修改是触发  数据马上变 但还没变
updated


			beforeUpdate: function() {
				console.log("beforeUpdate"+this.a)
			},
			updated: function() {
				console.log("updated"+this.a)
			
			},   
beforeUpdate 这里的之前还是之后， 是针对是否渲染到dom里。 data的数据实际都是更改后的。
updated

			beforeUpdate: function() {
				console.log("beforeUpdate"+this.a)   //都是更改后的。
			},
			updated: function() {
				console.log("updated"+this.a)
			
			},			
beforeDestroy	销毁  这里针对的是   当前app实例内dom 销毁。 单页面切换时，和v-if 为                 false时，页面销毁时 触发钩子函数。
destroyed
			beforeDestroy: function() {
				console.log('beforeDestroy')
			
			},
			destroyed:function() {
				
			}
            
            
 总结： vue 设计思路是单页面应用， 页面的切换都是 一个页面整体dom的销毁，和另一个页面dom的加载 ，所以每个页面的操作，都经历了从渲染到销毁的生命周期。
 v-if  有销毁，v-show 只是css  display:none.实质并没有销毁。
```

## 4. 组件的传值

```





```

## 5. 组件传值

### 5.1父传子

```js
1. 父传子  传值设计 props

		<div id="app">	
			<product-com v-for='item ,index in prolist' :fatherlist='item'>                </product-com>
		</div>


		Vue.component('product-com',{
			 props: ['fatherlist'],
			template: `
			<li>
			<h3>产品名称:{{fatherlist.title}}</h3>
			<h4>产品价格:{{fatherlist.price}}</h4>
			</li>
			`,
			data:function(){
				return{
					title:'三只松鼠'
				}
			},
			
			mounted:function(){
				// console.log(data)
				
			}
	
		})

		let app = new Vue({
			el: '#app',
			data: {
				prolist: [{
					title: '产品1',
					price: '10元'
				}, {
					title: '产品2',
					price: '12元'
				}, {
					title: '产品3',
					price: '13元'
				}, {
					title: '产品4',
					price: '16元'
				}, ]
			},
		})
	</script>
注意几点： 
1. 由于代码自上而下，所以组件先建立，再实例注册。
2.component  template：`` 模板，循环的部分一定要有一个最外的标签，vue只循环template的                  第一个闭合标签。
3.:fatherlist='item'  props: ['fatherlist'],字组件中准备指定变量保存来自父组件的数据。
4. 组件中的data 已返回值形式
	 data:function(){
				return{
					title:'三只松鼠'
				}
			}
例子2：
  HTML 中的 attribute 名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。这意味着当你使用 DOM 中的模板时，camelCase (驼峰命名法) 的 prop 名需要使用其等价的 kebab-case (短横线分隔命名) 命名
  查看  school-name

    <school school-name='静态数据-学校名字'></school>

	Vue.component('school',{
			 props: ['schoolName'],
			template: `	<li>schoolname :{{schoolName }}</li>`,
			data:function(){
				return{
					title:'三只松鼠'
				}
			}
		})

		let app = new Vue({
			el: '#app',
			data: {
			
			},

		})

```

### 5.2 关于组件 标签 传值

```
组件标签：

<school :dongname='动态数据-学校名字'></school>
注意的是：key 作为识别dom唯一性的属性，给vue 作为计算的。props的时候，不能作为值使用。
:key='index'


```

### 5.1父传子

```js
第二步 ：标签传入
<school v-for="item, index in fatherdata" :schoolName="item" :index='index' :key='index'></school>


Vue.component('school',{
			 props: ['schoolName','index'],//第三步  props指定变量 接受
			 //第四部：模板内使用变量
			template: `	<li>schoolname :{{schoolName }}--序号{{index}}</li>`,
			data:function(){
				return{
					title:'三只松鼠'
				}
			}
		})

		let app = new Vue({
			el: '#app',
			data: {
			fatherdata:['tom','bon','jem']  //父元素的数据第一步
			},

		})






```

### 父传子：   关键点 子组件 props 配置项

  原理： 

第一步： <o-a :name="fathemsg"></o-a>  ，父组件中 属性形式传入值。

第二步： o-a 子组件中，使用props name 属性值，接受。

第三步：   子组件--{{name}} 使用值

````javascript
// 父组件
<template>
    <div id="app">
        父组件--{{msg}}
        <!--绑定自定义属性，变量-->
        <o-a :name="msg"></o-a>
    </div>
</template>

<script>
import oA from '@/test/A'
export default{
    data(){
        return{
            msg:'TaylorSwift',
        }
    },
    components:{
        oA
    }
}

</script>




// 子组件

<template>
    <div id="app">
        子组件--{{name}}
    </div>
</template>

<script>
export default{
//  接收值
    props:{
        name:{
            type:String,
            default:0
        }
    },
    data(){
        return{
            
        }
    }
}
</script>

````





### 5.2 子传父$emit事件注册

```js
1.   html部分
			<school @childnameevet='fatherevent'  v-for="item, index in fatherdata" :school-name="item" :index='index' :key='index'></school>
		   你选择的是：{{chooseSchool}}

2.	 js部分
	Vue.component('school',{
			 props: ['schoolName','index'],
			template: `	<li>schoolname :{{schoolName }}--序号{{index}}
			  <button @click='childevet(schoolName)'> 选择学校</button>
			</li>`,
			data:function(){
				return{
					title:'三只松鼠'
				}
			},
			methods:{
				childevet:function(schoolName){
					this.$emit('childnameevet',schoolName)
					
				}
			}
		})

		let app = new Vue({
			el: '#app',
			data: {
			fatherdata:['清华','郑大','北大'],
			chooseSchool:''
			},
			methods:{
				fatherevent:function(data){
					this.chooseSchool=data
					console.log('触发父 事件')
				}
			}

		})
		第一步： 子组件内调用自己方法childevet
		第二步： 该方法 执行了 注册事件 并传了一个值 ，childnameevet变成了子组件标签上的一个点击属性。
        childevet:function(schoolName){
					this.$emit('childnameevet',schoolName)
				}    
		第三步： 定义的事件名字， 同时触发，条用了父级的方法，方法内接受了来自子组件的值，并修改了父级的data为新值准备的变量，存储新值。通知vue的视图监控到值得变化，即自动修改页面。
		
		
<school :action='fatherevent' v-for="item, index in fatherdata" :school-   name="item" :index='index' :key='index'></school>
			你选择的是：{{chooseSchool}}	
		
	js
    	Vue.component('school', {
			props: ['schoolName', 'index','action'],
			template: `	<li>schoolname :{{schoolName }}--序号{{index}}
			            <button @click='action(schoolName)'> 选择学校</button>
			</li>`,
			data: function() {
				return {
				}
			},
			methods: {
	
			}
		})

		let app = new Vue({
			el: '#app',
			data: {
				fatherdata: ['清华', '郑大', '北大'],
				chooseSchool: ''
			},
			methods: {
				fatherevent: function(data) {
					this.chooseSchool = data
					console.log('触发父 事件')
				}
			}

		})
		
 第二种方法： 把父级的方法函数，在子组件上以属性的形式，props接受，然后在子组件中     调      用。利用了this不变的特性。    子组件this 指component   父级 this 指vue实例
 第三种方法：
		 子组件传值与父组件，并调用。
		 原因是：component组件中的this中包含父级的内容和方法。
		 this.$parent.fatherevent(schoolName)
第四种方法：	
点击事件中直接调用父级方法。
		Vue.component('school', {
			props: ['schoolName', 'index','action'],
			template: `	<li>schoolname :{{schoolName }}--序号{{index}}
			   <button @click='$parent.fatherevent(schoolName)'> 选择学校</button>
			</li>`,
			data: function() {
				return {
				}
			},
			// methods: {
	  //            printthis:function(schoolName){
			
			// 		this.$parent.fatherevent(schoolName)
			// 	 } 	
			// }
		})
第五种：
同样利用  this.parent属性，直接改数值。
缺点：不适合传大量数据。
<button @click='$parent.chooseSchool=schoolName'> 选择学校</button>
	
第六种方法： 利用this里面的 @root 直接找到根组件vue,调用里面的方法和值。    
    
    注意：  根组件中有子组件， 子组件找那个有父组件，理论上可以直接修改值，但基于低耦合的初衷，还是建议props的方法获取。
    
    
```

## 子传父：

````javascript
子传父    $emit  事件。 
子元素 执行 this.$emit('close',this.flag);  close自定义的事件名称， 注册了一个close属性。
子组件的标签内，使用事件。 【 注意，写在子组件的标签内。】
在父元素的事件中，转移data值。  
 <o-a  @close='father_close'></o-a> 父组件中， 
  
   data(){
        return{
            msg:'我是父组件',
            flag:'待定',
            isvip:2
        }
    }
    
方法作用是，把接受到的值，转移到自己的数据data中。
father_close(val){
        this.flag = val;
    }


````

完整代码：

子

````javascript

<template>
    <div id="prduct">
        子组件 获取的父组件msg--{{name}}
        
    </div>
</template>

<script>
export default{
//  接收值
    props:{
        name:{
            type:String,
            default:0
        }
    },
    data(){
        return{
            flag:'我是子组件的值'
        }
    },
    methods:{
    },
    created(){
  
          this.$emit('close',this.flag);
    }
    
}
</script>

<style >

#prduct{
    border: 1px black solid;
}


</style>

````

父

````javascript
<template>
    <div id="Helloworld">
        父组件--{{msg}}
        <!--绑定自定义属性，变量-->
        <o-a :name="msg" @close='father_close'></o-a>

        <h1 >来自子组件的值  {{ flag }}</h1>
    </div>
</template>

<script>
import oA from '@/components/product'

export default{
    data(){
        return{
            msg:'我是父组件',
            flag:'待定',
            isvip:2
        }
    },
    components:{
        oA
    },
    mounted(){
      
 console.log(this);
    },
    methods:{

      
  father_close(val){
        this.flag = val;
    }
}}

</script>
<style>
#Helloworld{
    border: 1px red solid;
}
</style>
````











# 第四天：组件基础

## 1. 组件的插槽与v-model

```
输入框<input type="text" name="" id="" @input="username=$event.target.value" :value="username" />
 input内容改变就触发事件



```

### 1.1 组件的复用

```
组件标签可以放置多个，而不相互影响。
原因：
组件data 必须是一个函数 因此每个实例可以维护一份被返回对象的独立的拷贝：
data: function () {
  return {
    count: 0
  }
}
如果：
data: {
  count: 0
}  将相互影响。
```

### 1.2组件分类

```js
为了能在模板中使用，这些组件必须先注册以便 Vue 能够识别。这里有两种组件的注册类型：全局注册和局部注册。至此，我们的组件都只是通过 Vue.component 全局注册的：
全局注册
Vue.component('my-component-name', {
  // ... options ...
})
```

### 

```
详见上文
```

### 1.4 单个根元素

```
组件最外层要有一个父标签包裹否则：vue会提示
every component must have a single root element (每个组件必须只有一个根元素)

<h3>{{ title }}</h3>
<div v-html="content"></div>
```

### 1.5 监听子组件事件

```
详见上文
```

#### 1.5.1 在组件上使用v-model

```js
1. 标签上使用
<input v-model="searchText">
等价于
<input
  v-bind:value="searchText"
  v-on:input="searchText = $event.target.value"
>
2.当用在组件上时
   v-model 则会这样：   
 <custom-input
  v-bind:value="searchText"
  v-on:input="searchText = $event"
></custom-input>     
为了让它正常工作，这个组件内的 <input> 必须：

将其 value attribute 绑定到一个名叫 value 的 prop 上
在其 input 事件被触发时，将新的值通过自定义的 input 事件抛出
写成代码之后是这样的：

Vue.component('custom-input', {
  props: ['value'],
  template: `
    <input
      v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)"
    >
  `
})

区别原因是： 设计思想上针对结构不同的解决方案。
核心是  原生标签的 value  input 事件
```



### 1.6   vue双向传值案例

```js
html
			<custom-input :username_="username" @input='chengemsg'></custom-input>
		{{username}}

js
	<script type="text/javascript">
		Vue.component('custom-input', {
			props: ['username_'],
			template: ` 
				<div>子组件的输入框
			<input  v-on:input="$emit('input', $event.target.value)" :value='username_'>
			</div>`
		})

		var app = new Vue({
			el: '#app',
			data: {
				username: 'tom'
			},
			methods: {
				chengemsg: function(a) {
					this.username = a
				}
			}
		})
	</script>
解读：
 props: ['username_'], 是父传子值的标志。   
$emit('input', $event.target.value)" :value='username_'>   
        
$emit是注册成自定义事件使用，是子传父的标志。 事件用于调用父级的方法，以改变父级的值。
```

## 1.7 插槽

```
通过插槽分发内容
和 HTML 元素一样，我们经常需要向一个组件传递内容，像这样：
使用方法：
html部分：
			<alert-cont1 >
				<h2>小心老师</h2>
			</alert-cont1>
js部分：
Vue.component('alert-cont1', {
			props: ["html"],
			template: `
			<div class="alert">
				<h1>温馨提示</h1>
				<div class="content">
					<slot></slot>
				</div>
			</div>
			
			`
		})
注意两点： 1. 自定义组件标签，内容加入中间  2.  slot标签 定位容器位置。3. 自定义标签内可以使用{{html}}插值，引用父级的值。
```

### 命名插槽

````javascript
   父组件--{{msg}}
   
        <o-a :name="msg" @close='father_close'>
                <p slot="top"> top</p>
                <p slot="bottom">bottom</p>
        </o-a>
````



子组件

````javascript
<template>
    <div id="prduct">
        子组件 获取的父组件msg--{{name}}
       <slot name="top"></slot>

       <slot name="bottom"></slot>
    </div>
</template>
````

总结 :  子组件，会对应父组件的条件，  对应显示。

使用场景： tab bar 左中右 布局差不多的。   slot占位， 显示。



# 第五天

## 1.vue--cli 脚手架

```
文档位置：
     生态系统->  工具   vue-cli 

webpack的构建  基于nod.js   
自动化构建工具  打包和编译

命令
cd../  返回上一层
vue.ui   可视化创建项目

关系：
vue-cli  的核心是webpack。
的核心是webpack的核心是node
```

```
1.  检测vue 版本    
vue --version

2.  如果你已经全局安装了旧版本的 vue-cli (1.x 或 2.x)，你需要先通过 npm uninstall vue-cli -g 或    	yarn global remove vue-cli 卸载它。
3.  安装新包
     npm install -g @vue/cli   全局安装  //vue 版本从2.9.6  到4.3.1

创建项目

4.vue create testapp    创建项目  
    a. 选择手动创建
    b. 上下箭头选择  空格键确定 配置自己需要的模块   babel是编译
    c. 配置信息在一个文件中？  inpackage.json  //常用这个
    d. 是否保存此配置 下次用  y enter
    e. 去个名字
    f.这一步可能会有   yand  还是npm
    
 5.npm run serve  创建完成   

vue 创建步骤说明
第三步时：功能是，后端是否不管你进入那个页面都只返回首页。
? Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n) 
y  后端部署时要做操作。   路径上好看一点
n后端不用做处理。    路径上不好看一点

```

## vue页面式创建

```bash
命令
vue ui
 依次是取名字  选择依赖模块  选择是否手动创建     点击创建项目

 可以在可视化界面里插件  页面配置依赖功能  例如：axios 请求配置
可以执行打包  运行等操作

```

## 2.vue-devtools 浏览器插件安装和使用

```
介绍
vue-devtools是一款基于chrome游览器的插件，用于调试vue应用，这可以极大地提高我们的调试效率。接下来我们就介绍一下vue-devtools的安装。
这里vpn 借助工具jjqqkk软件




```

## 3. vue cli原理

```
需求点： html的依赖管理 js包的管理。
早期是 require.js 自定义方法，
项目中只需引入一个require.js 就行了。

1.准备定义路径     ajax请求回来，再做解析。
		require.config({
			paths: {
				"jquery": ["https://"]
			}
		})
		
		require(['jquery',function(){
			$(function(){
2. 使用				加载需要的js. 以下是需要使用的代码
				consoole.log('jquery已被加载')
				
			})
		}])


```

webpack安装和使用 指令

```
1.查看webpack版本
     webpack -v
2.安装
cnpm install webpack -g         这个是webpack   他们不是同一个东西。


npm install --save-dev webpack-cli -g      这个是webpack-cli 脚手架

清屏  clear

```

# 第六天

## 1.vue组件化

```
1.main.js中代码意思

import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
}).
render函数是vue通过js渲染dom结构的函数createElement，约定可以简写为h
2.

练习demo是 聊天模拟
组件之间的值和方法的 传递

引入知识：

socket    两方保持沟通。实时在线 tcp协议完成

http 只是 发送一次返回一个数据  两方没有练习。  除非长轮询：（ 没隔一段时间请求一次）
```

## 聊天项目略过

## 2. vue的原理

```
1.构造函数的声明

 ES6 Class 类
概述
在ES6中，class (类)作为对象的模板被引入，可以通过 class 关键字定义类。
class 的本质是 function。
它可以看作一个语法糖，让对象原型的写法更加清晰、更像面向对象编程的语法。

例子
class Polygon {
  constructor(height, width) {
    this.area = height * width;
  }
}

console.log(new Polygon(4, 3).area);
// expected output: 12

2.
employee
       constructor 属性返回对创建此对象的数组函数的引用。
3. 
Web 开发技术请参见 JavaScript请参见 JavaScript 参考请参见 JavaScript 标准内置对象请参见 ObjectObject.defineProperty()

Object.defineProperty() 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。

4. 
js对象的 set 和 get 用法
对象的 set get 是es5的中对象的特性，使用示例：

在初始化对象的时候这样使用
```

## 第一个： 数据代理

```js
<script type="text/javascript">
		class Vue {
			constructor(options) {
				//通过选择获取跟对象
				this.$el = document.querySelector(options.el)
				this.$options = options
				// 代理options的data数据
				for (let key in this.$options.data) {
					Object.defineProperty(this, key, {
						configurable: false,
						enumerable: true,
						get() {
							console.log(0)
							return this.$options.data[key]
						},
						set(val) {
							
							this.$options.data[key] = val
						}
					})
				}
			}
		}
	</script>
	<script type="text/javascript">
		let options = ({
			el: '#app',
			data: {
				msg: 'hello laocheng',
				username: '小明'
			},
			methods: {
				changeenent: function() {
					this.msg = 'hello vue'

				}
			}
		})

		let app = new Vue(options)
		
	</script>
        
  关键点：运用了 js方法： get set      设置属性和方法
        
```

第二个： 数据如何自动变化

```
标签的自带属性
元素类型
nodeTpe 节点类型

节点类型	nodeType	nodeName	nodeValue
元素节点	1	标签名（大写）	null               标签上可以带属性
属性节点	2	属性名	属性值
文本节点	3	#text	文本内容

HTML dom中常用的三种节点分别是元素节点、属性节点、文本节点。
例子
<h1 v-html="msg">  内容区</h1>
h1       元素节点
html="msg"   属性节点
容区             文本节点


```

### Object.defineProperty  方法的使用

需要添加属性的对象，你需要加的属性，配置项

```

		// Object.defineProperty阔以用于给对象添加更新属性
		let obj = {name:'小明'}
		// 该方法中包含以下参数：需要添加属性的对象，你需要加的属性，配置项
		Object.defineProperty(obj, 'name', {
		// getter函数
		get() {
		// get函数中，一定要return当前这个新添加进去的属性作为返回值
		console.log('你当前获取到的值是', name) // 相当于获取：obj.name
		return name
		},
		// setter函数, 这个函数中包含一个参数，这个参数表示当前设置的这个属性的新的值, 相当于:obj.name = 'itcast'
		set(newName) {
		name = newName
		console.log('这里你给name传递了新的值', newName);
		}
		})
```

vue中的this

```
             node.addEventListener('click',function(event){
							this.eventFn=this.$options.methods[vmkey].bind(this)
						console.log(this)   //this指向当前node 标签
						})
						
						
						
```

vue中的事件继承

```
         node.addEventListener('click',(event)=>{
							this.eventFn=this.$options.methods[vmkey].bind(this)  //复制到this  （即vue对象下）
						     this.eventFn()
						})
						
						
						
	this.eventFn(event)  效果等同于this.eventFn()					
						
```

# 第七天

## 1. css  详见收藏夹

vue    css预编译插件   

less sass   两种预编译插件   作用是 ：快捷开发   让css 像 js一样可以封装

## 2. 路由

### 2020.08.15 复习

1. router link

   <router-link to="/">Home</router-link>   router.js中配好路由，link就是a标签，点击修改浏览器地址。vue-router监控路由变化，切换页面的。单页面应用。

2.   router-view 

 使用routerview的情况，就是父页面的下面显示 局部子组件。

路由中需要配置如下：

​      path: '/HelloWorld',

​      name: 'HelloWorld',

​      component: HelloWorld,

​      children:[

​           { path: 'Layout1', component: Layout1 },

​         { path: 'Layout2', component: Layout2 },

​      ]

配合a 标签 控制浏览器路由变化

这样当前页面会显示两个组件。父组件和子组件。  子组件的位置显示由父组件中的 <router-view /> 标签位置控制。

<router-link to="/HelloWorld/Layout">Layout</router-link>







```
1. vue 实质： 监控路由是否变化  触发事件 渲染页面

2.
建立项目第一个处理问题是路由  histore      文章参考https://www.jianshu.com/p/4c5c99abb864
3. 配置选择路由后。实际上是

main.js中增加

import Vue from 'vue'
import App from './App.vue'
import router from './router'  //<-----这里

Vue.config.productionTip = false

new Vue({
  router,   //<-----这里
  render: h => h(App)
}).$mount('#app')

```

### 1 .router-link

```
1.   router-link     vue会渲染为a标签，并加上actve  并且a标签自带请求，会刷新页面。
           
           <div id="nav">
			<router-link to="/">Home</router-link> |
			<router-link to="/about">About</router-link>|
			<router-link to="/me">个人中心</router-link>
			<a href="/news">新闻中心</a>
		</div>
		
	大组件放到view中。 小组件放到components中
2.
import Mecon from '../views/Me.vue'

{
	 path: '/me',
	 // name: 'Me',
	 component:Mecon
  }
  
  不能是这样，mecon上面引入是个变量，加引号，变成字符串了。
  component：‘Mecon’
  
```

### 2.router-view

```
	<div id="app">
		<div id="nav">
			<router-link to="/">Home</router-link> |    <-- 点击事件 获取后面home
			<router-link to="/about">About</router-link>|
			<router-link to="/me">个人中心</router-link>
		</div>
		<router-view />     <-- 标签替换，组件内容放置区
	</div>
```

### 3.vue单页面 与net网路

```
只要打开第一个往页，后面都是本页面内的切换，也不会白屏，因为没有向后台请求。
```

### 4.两种路由方式

```

声明式	                             编程式
<router-link :to="...">       	router.push(...)


	export default{
		methods:{
			goAbout(){
				console.log(this.$router)
				// this.$router.push({ path: '/about'})
				this.$router.push('/about')
			}
		}
	}

官方：
// 字符串
router.push('home')

// 对象
router.push({ path: 'home' })

// 命名的路由
router.push({ name: 'user', params: { userId: '123' }})

// 带查询参数，变成 /register?plan=private
router.push({ path: 'register', query: { plan: 'private' }})

```

### 5.path传参

```
{
	  path:'/newvue/:newsid',
	  component:newVue
  }
  
  new页面
  {{this.$route.params.newsid}}
  
  http://localhost:8080/newvue/147
```

### 6. import 绝对路径

```
import Mecon from '../views/Me.vue'
import newVue from '@/views/newVue.vue'
@代表src    


```

### 7.axios的使用

```js
1.
 cnpm install axios --save
 2.单页面中引入import axios from 'axios'
3.

async beforeMount() {
			let key = '46e9f8418133439999dbba9aae51ddfc';
			let httpUrl = `https://free-api.heweather.net/s6/weather/now?location=${this.$route.params.city}&key=${key}`
			let res
			let data
			// try{
			// 	 res = await axios.get(httpUrl)
			// }catch(error){
			// 	console.log(error)
			// }
			axios.get(httpUrl).then((res)=>{
				console.log(res)
				res.data.HeWeather6[0].now?data = res.data.HeWeather6[0].now:''			
					this.$route.params.city?this.city = this.$route.params.city:alert(0)
					data.wind_dir?this.wind_dir = data.wind_dir:this.wind_dir='默认1'
					this.cond_txt = data.cond_txt
			},(err)=>{
				cosole.log(err)
			})	
		},

```

### 8.路由传参

```
路由传参
路由传递多个值，会在$route对象下挂载数组。
{
	  path:'/weather/:city/:area',
	  component:weather
  }

http://localhost:8080/weather/beijing/tongzhou

this.$route.params

{city: "beijing", area: "tongzhou"}
area: "tongzhou"
city: "beijing"
```

### 9.响应路由参数的变化 动态路由



当使用路由参数时，例如从 `/user/foo` 导航到 `/user/bar`，**原来的组件实例会被复用**。因为两个路由都渲染同个组件，比起销毁再创建，复用则显得更加高效。**不过，这也意味着组件的生命周期钩子不会再被调用**。

复用组件时，想对路由参数的变化作出响应的话，你可以简单地 watch (监测变化) `$route` 对象：



动态路由：随匹配路径变化，切换不同页面，同时：后面的值也能拿到。

```
const User = {
  template: '...',
  watch: {
    $route(to, from) {
      // 对路由变化作出响应...
    }
  }
}
写在script中 监控从哪到哪
	export default {
		watch: {
			$route(to, from) {
				// 对路由变化作出响应...
				console.log(to)
			},
		}
	}

```

### 10.嵌套路由

新闻页面之下 ，包含本地新闻， 其他地方新闻版块。children 路由

```

1.
{
	  path:'/bignew',
	  component:bignew,
	  children: [
	          // 当 /user/:id 匹配成功，
	          // UserHome 会被渲染在 User 的 <router-view> 中
	          { path: 'imgnew', component: imgnew },
	          { path: 'viewnew', component: viewnew }
	        ]
  }
  注意：children  中path 没有/
  
  2.   父页面下放置路由出口
  <router-view />
  
  
  path:'/bignew/:id',
  
  http://localhost:8080/bignew/300/viewnew
  
  动态路由和嵌套路由可以一块用，并且可以拿到值。
  
  params:
id: "300"
  
```

# 第八天

## 路由传参汇总

## 1.编程式的导航push



![img](https://upload-images.jianshu.io/upload_images/2891127-0cf4af08a88850ae.png?imageMogr2/auto-orient/strip|imageView2/2/w/927/format/webp)除了使用 `<router-link>` 创建 a 标签来定义导航链接，我们还可以借助 router 的实例方法，通过编写代码来实现想要导航到不同的 URL，则使用 `router.push` 方法。这个方法会向 history 栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，则回到之前的 URL。

当你点击 `<router-link>` 时，这个方法会在内部调用，所以说，点击 `<router-link :to="...">` 等同于调用 `router.push(...)`。

```
1.           声明式	            编程式
<router-link :to="...">	     router.push(...)

该方法的参数可以是一个字符串路径，或者一个描述地址的对象。例如：

// 字符串
router.push('home')

// 对象
router.push({ path: 'home' })

// 命名的路由
router.push({ name: 'user', params: { userId: '123' }})

// 带查询参数，变成 /register?plan=private
router.push({ path: 'register', query: { plan: 'private' }})
2.

第一种的传参还可以这样传
this.$router.push('/about?uername=laocheng&passwprd=123')
console.log(this.$router)//后台会存储在query数组上.
3.
push 可以加入回调函数 用于执行改换路由后的 操作
	this.$router.push(
				{path:'/about'},function(){
					console.log('push了')
				})

```

## 2.编程式的导航`replace`

跟 `router.push` 很像，唯一的不同就是，它不会向 history 添加新记录，而是跟它的方法名一样 —— 替换掉当前的 history 记录

```
router.replace(location, onComplete?, onAbort?)
                             回调函数     失败函数  
1. replace加上回调

this.$router.replace(
				{path:'/about'},
				function(){
					console.log("已替换页面")
				})
```

## 3.router.go(n)

```
#router.go(n)
这个方法的参数是一个整数，意思是在 history 记录中向前或者后退多少步，类似

// 在浏览器记录中前进一步，等同于 history.forward()
router.go(1)

// 后退一步记录，等同于 history.back()
router.go(-1)

// 前进 3 步记录
router.go(3)

// 如果 history 记录不够用，那就默默地失败呗
router.go(-100)
router.go(100)
```

## 4.命名路由

```
1.
const router = new VueRouter({
  routes: [
    {
      path: '/user/:userId',
      name: 'user',
      component: User
    }
  ]
})


要链接到一个命名路由，可以给 router-link 的 to 属性传一个对象：

<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>

利用name 做跳转
```

## 5. 命名视图

```
功能是： 一个页面中显示三个组件  
导航  左侧栏    右侧内容区

 1. 
  路由中js中配置components 
 {
    path: '/',
    name: 'Home',
	components:{
		default:Home,
		top:Top,
		aside:Aside,
	}
  },
  
2.
<div id="app">
    <div id="nav">
    </div>
	<router-view  name="aside"></router-view>
	 <router-view/>
  </div>
  
  	 <router-view/>  注意，路由视口只能在app中显示 。  如果在其他页面引用组件， 
  
 

```

## 6.重定向和别名

```
1.重定向
重定向也是通过 routes 配置来完成，下面例子是从 /a 重定向到 /b：
例子
  { path: '/aa', redirect: '/about' },  
http://localhost:8080/#/aa   同样进入/about

2.
http://localhost:8080/#/about?id=00
?号后面的值，会存储到this.$route的query:  id: "00" 中
3.
http://localhost:8080/#/aa?id=1
可以通过？传参，判断路由导向。并且可以在新转的路由上传递新的参数。
 { path: '/aa', redirect: (to)=>{
	 
	if(to.query.id=1){
		return{name:'Top',params:{name:"00000"}}
	}else{
		return{{name:'news'}}
	}	
	
  } },
  
```

## 别名

```
1.
http://localhost:8080/#/self
就是访问本名字和小名字， 都指向同一个组件。与重定向的区别是地址上的显示别名保持自己的别名字。
 {
	  path:'/Top',
	  name:"Top",
	   alias:"/self",
	  component:Top
	 
  },

```

# 第九天

## 1.组件传参 （就是router传参另一种方法-解耦）

```
 参数  props: true
 
1. http://localhost:8080/#/Top/lisy    注意不要是name=lisy
 
2. {
	  path:'/Top/:name',
	  name:"Top",
	   alias:"/self", //别名
	  component:Top,
	  props: true
	 
  },
  
 3. top组件中 准备键值
  props: ['name'],
  
  
4.
this 下查看
$props: Object
name: "lisy"


对props数据进行处理


{
		path: '/Top/:name',
		name: "Top",
		alias: "/self",
		component: Top,
		// props: true
		props: (route) => ({
			years: 20,
			name:route.params.name

		})

	},
显示
$props: Object
name: "lis"
years: 20

```

## 2.HTML5 History 模式

```

当你使用 history 模式时，URL 就像正常的 url，例如 http://yoursite.com/user/id，也好看！

history 模式时
上面就是说，vue是单页面， 不管发送什么地址，都只会返回一个index页面，想要模拟访问那个页面，返回那个页面，后台需要处理。
```

## 3.路由高级    路由元信息

```

指的是：往一组路由中 加入一个 meta: { requiresAuth: true }，用于记录这一个路由与其他路由不同之处。
         比如：是否允许登陆， 权限，
{path: '/Top/:name',
component: Top}

当在路由中配置信息后，meta信息会挂载到会暴露为 $route 对象 下面
使用场景： 进入本路由的时候判断一下，是否是VIP,有没有权限浏览。
{
		path: '/Top',
		component: Top,
		meta: {
			isAuth: true,
			needlogin: true,
			content: 'this is shouye'
		}
	},
```

## 4.路由过渡

```
1.
npm install animate.css --save
2.
import  'animate.css'   main.js中引入
3.   在以下4中情况下使用
    Vue 提供了 transition 的封装组件，在下列情形中，可以给任何元素和组件添加进入/离开过渡
条件渲染 (使用 v-if)
条件展示 (使用 v-show)
动态组件
组件根节点
4.  加name属性   transition会自动拼接 进入 和离开class 
   <transition name="bounce" >
			<router-view />
		</transition>
5.
	@-webkit-keyframes bounce-in {
		20% {
			opacity: 1;
			transform: translate3d(-20px, 0, 0) scaleX(0.9);
		}

		to {
			opacity: 0;
			transform: translate3d(2000px, 0, 0) scaleX(2);
		}
	}

	.bounce-enter-active {
		animation: bounce-in 3s;
	

	.bounce-leave-active {
		animation: bounce-in 1s reverse;
	}
```

```
遗留问题：
在vue 服务器状态下， 自定义类名失败。
  <transition
    name="custom-classes-transition"
    enter-active-class="animated tada"
    leave-active-class="animated bounceOutRight"
  >
    <p v-if="show">hello</p>
  </transition>



```

#### 过渡模式

```
同时生效的进入和离开的过渡不能满足所有要求，所以 Vue 提供了过渡模式

in-out：新元素先进行过渡，完成之后当前元素过渡离开。

out-in：当前元素先进行过渡，完成之后新元素过渡进入。

用 out-in 重写之前的开关按钮过渡：

作用是：改变两个页面过渡的先后顺序
	<transition name="bounce" mode="out-in">
			<router-view />
		</transition>
```

## 5.进阶 数据获取beforeRouteEnter

```

类似于钩子函数， 只不过这次对象是以路由进入前后做判断
进入前和

1.beforeRouteEnter(to, from, next) {
			console.log(to, from, next)
			// getPost(to.params.id, (err, post) => {
			// 	next(vm => vm.setData(err, post))
			// })
		},
		// 路由改变前，组件就已经渲染完了
		// 逻辑稍稍不同
2.	beforeRouteUpdate(to, from, next) {
				console.log(to, from, next)
			this.post = null
			// getPost(to.params.id, (err, post) => {
			// 	this.setData(err, post)
			// 	next()
			// })
		},

对beforeRouteUpdate	的解释：
使用场景：
　　组件复用；路由跳转；
beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },

```

## 6.缓存页面keep-alive

```
 
              <keep-alive>
				<router-view />
			</keep-alive>
			
			
```

## 7.滚动行为

```
1.指的是当浏览b页面滚动到中间， 浏览器后退a页面， 然后再前进到b页面， 此时 b页面保持滚动到中间位置。
注意： 如果路由视口有过渡动画， 注意scrollBehavior路由滚动，需要设置延时。因为只有页面渲染出来后，才能滚动。
2.
VueRouter实例中放置参数scrollBehavior，在切换路由时，执行。

const router = new VueRouter({
	routes,
	scrollBehavior (to, from, savedPosition) {
	    // return 期望滚动到哪个的位置
		console.log(savedPosition)
		if (to.path=='/list'){
			// return{
			// 	x:savedPosition.x,
			// 	y:savedPosition.y
			// }
			window.scrollTo(0,savedPosition.y)   //使用原生方法也可以
		}
	
	  } 
})
```

8.路由懒加载

vue-cli   采用webpack 构建 ，pack中有个模块打包缓存功能。故这里也可以用。

```
场景是:打包一个页面较小，可以多个打包到一起。
 /* webpackChunkName: "about" */  后面的名字一样，就认为是同一个。
 这样在加载about的同时，也把Me加载上。
{
		path: '/about',
		name: 'About',
		component: () => import( /* webpackChunkName: "about" */ '../views/About.vue')
	},{
		path: '/Me',
		name: 'Me',
		component: () => import( /* webpackChunkName: "about" */ '../views/Me.vue')
	},
	
	
	
	
```

## 8 导航守卫（也叫路由守卫）

```
路由：
1.vue是单页面
2.路由不断切换，达到浏览展示作用。
导航事件：  就是在路由切换触发为节点，之前或者之后，做一些处理。
导航守卫就是路由事件。

const router = new VueRouter({ ... })
router.beforeEach((to, from, next) => {
  // ...
})
```

案例：

### 全局前置守卫beforeEach

```
1. 做了一个功能。 就是只要没登录，就跳转登陆页
router.beforeEach((to, from, next) => {
  console.log('----beforeEach-----')
   console.log(from ,to)
 
 let islogin=false;
 if(islogin||to.path=='/login'){
	 next()
 }else{
	 next({
		 path:'/login'
	 })
 }
})

需要注意的是：next
她是一个方法， next() 就是继续。 传入false,就是阻止，效果是，点击没有反应。 传入true，就是允许。


```

### 全局后置钩子router.afterEach

```
后置钩子的使用场景：
后置的比如页面浏览完毕后，用户跳转离开，所以可以吧浏览时间发送后台。


你也可以注册全局后置钩子，然而和守卫不同的是，这些钩子不会接受 next 函数也不会改变导航本身：

router.afterEach((to, from) => {
  // ...
})
```

### 路由独享的守卫beforeEnter

就是针对单一路由进行判断，写在对应的路由里面    使用参数beforeEnter

```
  {
    path: '/about',
    name: 'About',
    component: () => import(/* webpackChunkName: "about" */ '../views/About.vue'),
	beforeEnter: (to, from, next) => {
		alert('你没有权限')
	        next(false)
	      }
  }
```

### 组件内守卫beforeRouteEnter

类似于 钩子函数，只不过对象是路由的跳转前后而言，并且这个是放在某一个组件内判断，同全局的效果一样。

但配置的钩子不同，注意区分。 

```js
export default{
		beforeRouteEnter (to, from, next) {
					alert('你没有权限')
					next(true)
		    // 在渲染该组件的对应路由被 confirm 前调用
		    // 不！能！获取组件实例 `this`
		    // 因为当守卫执行前，组件实例还没被创建
		  },
		  beforeRouteUpdate (to, from, next) {
		    // 在当前路由改变，但是该组件被复用时调用
		    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
		    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
		    // 可以访问组件实例 `this`
		  },
		  beforeRouteLeave (to, from, next) {
			  console.log('离开了')
			  next()
		    // 导航离开该组件的对应路由时调用
		    // 可以访问组件实例 `this`
		  }
	}
```

# 第十天

## 1.axios

##### 引入postman chrome插件使用

```
定位：axios  是一个请求库，
可以做爬虫，nood结合。
学习目标是：不用死记。 会使用api.
http://www.axios-js.com/
Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。

1.安装
  npm install axios
2.router  indexjs
// 请求
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(VueAxios, axios)
3.使用页面中引入
	import axios from 'axios';
4.使用

			gethandle() {
		console.log('执行了')
				let url='https://api.heweather.net/s6/weather/grid-now?'
				axios.get(url, {
				    params: {
					location:'116.40,39.9',
				       key:'46e9f8418133439999dbba9aae51ddfc'
				    }	
				  })
				  .then(function (response) {
				    console.log(response);
				  })
				  .catch(function (error) {
				    console.log(error);
				  });	
			}
		

拦截器
在请求或响应被 then 或 catch 处理前拦截它们。


需要核实一下：全局引入后 组件内应该可以不用引入


在为引入axio是，可以使用原生请求 fetch
它是原生对象，浏览器一般自带。
	actions: {
		setDZ: function(content) {
			let httpURL = 'https://www.apiopen.top/getJoke?page=1&count=2&type=text'
			fetch(httpURL).then(res => res.json()).then(res => {
				console.log(content)
				// 通过muation来设置state
				content.commit('setDuanzi',res.result)
			})
		}
	},
```

## 4个取值的捷径方法

```
import {mapGetters,mapState,mapActions,mapMutations} from 'vuex'

这4个方法是vuex内置方法。
mapState  取data(state)值得
mapGetters  取getters 计算属性的值得
mapMutations 取mutations里面的方法
mapActions  取actions里面的方法

结构的时候： 方法类放到method里。 数据和计算属性放到组件计算属性里，因为要用他的值。
方法放到计算属性类肯定会自动调用的。

```



## 2.vuex  数据仓库   对应vue下$store

项目使用：

注意区分： 方法分两种。

同步方法：  mutations

 异步放啊： actions

 两个方法触发方式不同。 作用不同。   多用于触发异步，  异步中触发同步，同步触发data， 再到计算属性

。

 使用vuex中的 data数据    案例：   alert(this.state.a)



vuex是一个单独的对象，就想rourer一样。这里vuex中的this指向自己vuex (对象中 包含自己的配置项)

```
1.
vuex  数据仓库  全局数据和方法  数据剥离出来
哪些需要剥离出来： 多组件共用的数据和方法。

Vuex 可以帮助我们管理共享状态，并附带了更多的概念和框架。这需要对短期和长期效益进行权衡。
中小型项目不用引入vuex， 因为他会更复杂化。 大型项目数据较多，组件共用数据比较复杂，则不可避免要使用。



1.什么情况下使用vuex 
组件多   
多组件共用

2.仓库的标准配置项；
export default new Vuex.Store({
	//相当于data
  state: {
  
  },
  //相当于 store 的计算属性
  getters:{

  },
  //相当于methods
  mutations: {
  },
  //异步方法
  actions: {
  },
  //模块
  modules: {
  }
})


```

## 2.1实现原理 state

```js
1.vuex引入后的作用
Vuex 提供了一个从根组件向所有子组件，以 store 选项的方式“注入”该 store 的机制：
就是说，vuex将自己的数据方法挂载到了vue实例之下，（挂载到了vue 实例下面 ）在每个页面都可以拿到数据仓库的值,还有一个方法commit。
(commit:注意： 组建中调用仓库方法的手段；同时在仓库中异步调用同文件中同步方法，也是这个。)
注意： 数据会挂载到vue实例下的store

2.  vuexjs中 => Store页面
写入一个mum值，和一个调动方法。addNum
export default new Vuex.Store({
	//data
  state: {
	  num:0    <--这里
  },
  //methods
  mutations: {
	  addNum:function(state){   <--这里
		  this.state.num+=2
	  }
  },
  //异步方法
  actions: {
  },
  //模块
  modules: {
  }
})

3. 在home组建中使用仓库的----方法。 
  这样  $store.state.num
  同时在本组件中有一个方法 emitAction（），在本组件中触发this.$store.commit('addNum')，注意addNum是数据仓库中的方法。点击数据更改。 流程完毕。  vue tool中也可以查看数据触发者，事件，方法。
  【this.$store.commit('addNum')  还可以传值。this.$store.commit('addNum' ，‘data/methed’),不仅可以调用仓库的方法，还可以携带参数或者方法】
  
 
  
  
 emitAction: function(state) {
				this.$store.commit('addNum')//  跨页面调用同步方法。调用异步用dispatch
			}
	
视图中的dom    
<h1> store里的data:{{$store.state.num}} </h1>
<button @click="emitAction">点击加数</button>
4.在home组建中使用仓库的---值。

另一种简洁方式取值和方法：
设计者给出配置项
mapState 辅助函数

方式 
使用组件中写入：
	import {mapState} from 'vuex'
let mpastatedata=mapState(['msg','num'])
	
computed: {//在计算属性中解构
			// 使用对象展开运算符将 getter 混入 computed 对象中
			// ...mapGetters(['reverseMsg','mixinMsg'])
			...mpastatedata
		}

然后 组件中直接{{msg}}插值使用  num

```

## 2.2  getters store 的计算属性

第一种方式



```
1. Q:为什么store里面也设计一个计算属性，组建中不是也有吗？
   A: store作为公共仓库，各个页面都可以使用，组件中的计算属性只能用于本组件。
 引入getters 属性， 对仓库中的数据，已返回函数的形式，进行计算。并在 挂载到this.$store下。

store. js代码如下
state: {
	  num:0,
	  msg:"yunxiao"
  },
  // store 的计算属性
  getters:{
	  reversen:function(state){
		  return state.msg.split('').reverse('').join('')		 
	  }
  }, 
 
 
 使用用方式：
{{this.$store.getters.reversen}}



2.  组件中使用store 中的data数据同时传参操作

store js

  getters:{
	  mixinMsg:function(state){
	  		 return function(val){
				  return val+state.msg.split('').join('')+'自己添加的'
			 }		 
	  }
  },

使用页面
<h1> store里的data:{{this.$store .getters.mixinMsg(90)}} </h1><br>

```

### `第二种方式 mapGetters` 辅助函数

`mapGetters` 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性：

```
import { mapGetters } from 'vuex' <--引入
export default{
计算属性//
	 computed: {
	  // 使用对象展开运算符将 getter 混入 computed 对象中
	    ...mapGetters([
	      'reversen',
	     'unreversen'
	      // ...
	    ])
	  }
}


```

## 2.3  Mutation

## Mutation 必须是同步函数

```
更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。Vuex 中的 mutation 非常类似于事件：每个 mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。这个回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数


1.  这是仓库里的配置项啊
在这里边设置的方法，默认第一项是vuex的对象，里面有所有的已经写入的配置方法和data数据。
//异步方法
	actions: {
		setDZ: function(content) {
			let httpURL = 'https://www.apiopen.top/getJoke?page=1&count=2&type=text'
			fetch(httpURL).then(res => res.json()).then(res => {
				console.log(content)
				// 通过muation来设置state
				content.commit('setDuanzi',res.result)
			})
		}
	},





```



## 2.4  actions异步函数

```
作用是：ajxa 请求数据，赋值给state  （data),渲染到页面。
但是设计执行的流程是：  actions 里的方法

Action 提交的是 mutation，而不是直接变更状态

组建中条用仓库的异步方法：
在本页面建立点击事件，触发dispatch('setDZ')，来执行仓库的方法。
methods:{
			getduanzi:function(context){
				this.$store.dispatch('setDZ')
			}
			
		},

仓库代码：
//methods
	mutations: {
		addNum: function(state) {
			state.num += 2
		},
		setDuanzi:function(state,value){
			state.duanzi=value
			// console.log('我是store里的')
			// console.log(this.state)
		}

	},
	//异步方法
	actions: {
		setDZ(content) {// 原来写的是funtion(){}  一直报错.注意看官方案例
			let httpURL = 'https://www.apiopen.top/getJoke?page=1&count=2&type=text'
			fetch(httpURL).then(res => res.json()).then(res => {
				// console.log(content)
				// 通过muation来设置state
				content.commit('setDuanzi',res.result)
			})
		},



```

### 问题遗留：

```
我采用上面的方式引入，setDZ方法自动执行。采用官方的方法才正常。后面看一下问题

原因是：看上面
computed 可能是他自动执行了。底层代码的逻辑。

<script>
	import {mapGetters,mapState,mapActions,mapMutations} from 'vuex'

	// let mapGetdata=mapGetters(['reverseMsg','mixinMsg'])// 引入计算属性getters
	let mapStateobj=mapState(['msg','num','duanzi'])//引入数据state
	// let mapActionsobj=mapActions(['setDZ'])
	// let mapMutationsobj=mapMutations(['addNum'])
	
	export default {
		data() {
			return {
				message: '1234',
				// reversname:''
			}
		},
		// 8个钩子函数
		mounted() {
			console.log(this.$store)
		},	
		// 方法
		methods:{
			getduanzi:function(context){
				// this.$store.dispatch('setDZ')
			},
			 ...mapMutations({
			      add: 'someMutation', // 将 `this.add()` 映射为 `this.$store.commit('increment')`
			   addNum:"addNum"
				}),
				...mapActions({
				     setDZ: 'setDZ', 
				 
								})
			
		},
		// 计算属性
		computed: {
			// 使用对象展开运算符将 getter 混入 computed 对象中
			// ...mapGetters(['reverseMsg','mixinMsg'])
			...mapStateobj,
			// ...mpastatedata,
			// ...mapActionsobj,
			// ...mapMutationsobj
		}
	}
</script>

```

# 第十一天

## 1.vuex-插件  混合模式 混入

```
1.  知识背景：混合模式 引入配置项mixins，自己写options，然后以数据形式，注册到app实例中。
数据正常使用
<h1>{{num}}</h1>// 如果外面的数据和实例中的数据相同， 以实例中的为准，权重较高。例如：num: 100


	let options = {  //混入的配置项也要遵循规则
			data: {
				num: 100
			},
			created: function() {
				console.log('vue生命周期created')
			},
			mounted: function() {
				console.log('vue生命周期mounted')
			}
		}
		let app = new Vue({
			el: "#app",
			data: {num: 200},
			methods: {},
			mixins: [options],
		})

组建中也可以混入：
注意：options中的data以返回值的形式
1.定义组件：
Vue.component("child-element",{
			template:"<div>{{msg}}</div>",
			mixins:[options2]
		})
2.
	<div class="" id="app">
			<h1>{{num}}</h1>
			<child-element></child-element>
		</div>
```

## 2.自定义指令

```
v-focus自定义指令： 这就是属性 标签上特有的属性。

1. 自定义 input 自动选中事件
知识背景：Vue.directive 自定义配置

  然后你可以在模板中任何元素上使用新的 v-focus property，如下：
         <div class="" id="app">
			<input v-focus>
		</div>
		
		
		// 注册一个全局自定义指令 `v-focus`
		Vue.directive('focus', {
			// 当被绑定的元素插入到 DOM 中时……被调用
			inserted: function(el) {
				// 聚焦元素
				console.log(el)
				el.focus()
			}
		})





```

## 2.1自定义指令的生命周期

```
	// 注册一个全局自定义指令 `v-focus`
		Vue.directive('focus', {
			bind: function() {//只调用一次，指令第一次绑定到元素时调用
			},
			inserted: function(el) { // 当被绑定的元素插入到 DOM 中时……
				// 聚焦元素
				el.focus()
			
			},
			update: function() {//所在组件的 VNode 更新时调用
		
			},
			componentUpdated: function() {//子组件和父组件都更新时调用
			
			},
			unbind: function() {//只调用一次，指令与元素解绑时调用
		
			},
			
		})

2. 钩子函数的参数
  每个生命周期为了便于用户自定义事件 ， 提供了5个参数。 用这些参数构建自己的事件。
			inserted: function(el, binding, vnode, oldVnode) {
				el.focus()
				console.log("el")
				console.log(el)
					console.log("binding")
				console.log(binding)
				console.log("vnode")
				console.log(vnode)
				console.log("oldVnode")
				console.log(oldVnode)
			},





```

## 2.2 vue.use() 做了什么

```
1.通过全局方法 Vue.use() 使用插件的标志


2.插件通常用来为 Vue 添加全局功能。插件的功能范围没有严格的限制——一般有下面几种：

添加全局方法或者 property。如：vue-custom-element

添加全局资源：指令/过滤器/过渡等。如 vue-touch

通过全局混入来添加一些组件选项。如 vue-router

添加 Vue 实例方法，通过把它们添加到 Vue.prototype 上实现。

一个库，提供自己的 API，同时提供上面提到的一个或多个功能。如 vue-router
3. 自定义插件 并安装

	<div id="app">
			<h1 v-myfocus>插件</h1>
		</div>

<script type="text/javascript">
		let lyxcj = {
			install: function() {
				console.log('000')
				// 1. 添加全局方法或 property
					Vue.bgColor='skyblue'
				Vue.changeBg = function() {
				
					document.body.style.background = Vue.bgColor
				}

				// 2. 添加全局资源
				Vue.directive('myfocus', {
					bind(el, binding, vnode, oldVnode) {
						console.log(el)
					el.innerHTML='<h1>添加全局资源</h1>'
					}
			
				})

				// 3. 注入组件选项
				Vue.mixin({
					created: function() {
					console.log('这是注入的生命周期')
						}
					
				})

				// 4. 添加实例方法
				Vue.prototype.$changeBgcolor = function(methodOptions) {
					alert(0)
				document.body.style.background = 'skyblue'
				}


			}
		}
		Vue.use(lyxcj) //// 调用 `lc.install(Vue)`

		let app = new Vue({
			el: "#app"
		})
	</script>

注意：浏览器调试页面调用方法：
app.$changeBgcolor()，不加（）显示的只是function

```

## 3.过滤器

```js
简单的数据处理：可以用过滤器的功能，复杂的可以用计算属性。  |标志
{{msg | msgFilter}}
Vue.js 允许你自定义过滤器，可被用于一些常见的文本格式化。过滤器可以用在两个地方：双花括号插值和 v-bind 表达式 (后者从 2.1.0+ 开始支持)。过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符号指示：

<!-- 在双花括号中 -->
{{ message | capitalize }}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="rawId | formatId"></div>

当全局过滤器和局部过滤器重名时，会采用局部过滤器。
过滤器可以串联：{{ message | filterA | filterB }}


过滤器：消耗性能达，每次都要计算。计算属性:计算一次，存到内存里，性能消耗小。
案例：
		<div id="app">
			<h1>过滤器</h1>
			<h1>{{msg|msgFlter}}</h1>
		</div>

	<script type="text/javascript">
		Vue.filter('msgFlter',(val)=>{
			//传入msg参数
			return val.split('').reverse().join('')
		})
		let app = new Vue({
			el: "#app",
			data:{
				msg:"123456",
			
			}
		})
	</script>






```



# 补充：

### nextTick

```
  
  this.$nextTick(() => {
					    //设备运行正常率较高的企业排名
					    creatChart(res.data.data)
					})
```



# 复习：08.1 

#### Vue组件中的方法书写顺序

```
    - components   
    - props    
    - data     
    - created
    - mounted
    - activited
    - update
    - beforeRouteUpdate
    - methods   
    - filter
    - computed
    - watch
```





## 1  判断显示

````javascript
<div>
    <p v-if="isvip">是</p>
    <p v-else>他不是</p>
</div>

data： 中控制isvip的true 和false

````

## 2 故障排除

1. ​    现象，某个组件语法错误，导致整个页面空白。  分析： 组件是模块化，互补影响的，如果出现影响整个页面， 说明 当前使用的页面，引入了故障页面。  比如 路由页面引入了，代码错误，停止执行。

## 3  练习

````javascript

父传子
<child :child='up'></child>


子传父

 created(){
  
          this.$emit('close',this.flag);
    }

------------------ 上面是子-------------------------

 <child :child='up' @close='father_event'></child>


    methods: {
    father_event(data){
        console.log(data);
    }}
------------------ 上面是父-------------------------
    子元素注册事件， 他会自动 执行父元素的方法 father_event， 父元素获得data后， 转移到自己的数据仓库中。
````



## 4 vuex 复习

关键词  ：

state       mapState

getters     mapGetters

mutations    mapMutations

actions            mapactions

modules

```
2.仓库的标准配置项；
export default new Vuex.Store({
	//相当于data
  state: {
  
  },
  //相当于 store 的计算属性
  getters:{

  },
  //相当于methods
  mutations: {
  },
  //异步方法
  actions: {
  },
  //模块
  modules: {
  }
})
```

对应的方法：

````javascript
<template>
  <div>
    <p>{{ city1 }}</p>
    <p>{{ docubleCity }}</p>
  </div>
</template>
 
<script>
import { mapState,mapGetters,mapMutations } from 'vuex'
export default {
  data() {
    return {
 
    }
  },
  computed:{
    // 引入方式，以下两种皆可
    // 1.数组方式：
    ...mapState(['city']),
    ...mapGetters(['docubleCity'])
    
    // 2.对象方式：
    // ...mapState({
    //   city1:'city'
    // }),
    // ...mapGetters({
    //   docubleCity:'docubleCity'
    // })
  },
  methods:{
    ...mapMutations(['changeCity'])
  },
  mounted(){
    this.changeCity('贵州')
  }
};
</script>
````



vuex里有这么一个规则：只能在mutaions里修改state，actions不能直接修改state .[ 同步方法可以直接修改stats, 异步方法不能直接修改，异步可以执行同步的方法，间接修改stats。  ]



# 1. vuex简介

vuex是专门用来管理vue.js应用程序中状态的一个插件。他的作用是将应用中的所有状态都放在一起，集中式来管理。需要声明的是，这里所说的状态指的是vue组件中data里面的属性。了解vue的同学应该是明白data是怎么回事的吧，如果不懂的话，建议先学完vue的基础知识再看vuex。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6L2lidVdCSmM2bUdWNm8yQ2liZzRZY2pONTdpYVpIVkMwSFM2ckp6aWJoOGRHNXU3Y0h5TGJReHRzT2h3MUI2VGxPaWJjTkQ5QWtzZzRUUDhKamRDSXVNaWNtSEVRLzY0MD93eF9mbXQ9b3RoZXI)

https://me.csdn.net/yusirxiaer     Vuex的全面用法总结

# vue 引入并使用 vuex

## 1.安装

````javascript
npm install --save vuex
````

## 2.vuex准备

````javascript
// （1）在src目录下，创建一个文件夹，并命名为 store
// （2）在store目录下，创建index.js，内容如下：
 
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)
 
export default new Vuex.Store({
  state:{
    city:'广州'
  },
  mutations:{
    changeCity(state, city){
      state.city = city
    }
  },
  actions:{},
  getters:{
    docubleCity(state){
      return state.city +' '+ state.city
    }
  }
})
````



## 3.vue项目中引入

````javascript
// 在main.js中引入
import Vue from 'vue'
import App from './App'
import router from './router'

import store from './store'
 
 
/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  store,
  components: { App },
  template: '<App/>'
})
````



## 4.使用

````javascript
<template>
  <div>
    <p>{{ city }}</p>
    <p>{{ docubleCity }}</p>
  </div>
</template>
 
<script>
import { mapState,mapGetters,mapMutations } from 'vuex'
export default {
  data() {
    return {
 
    }
  },
  computed:{
    // 引入方式，以下两种皆可
    // 1.数组方式：
    // ...mapState(['city']),
    // ...mapGetters(['docubleCity'])
    
    // 2.对象方式：
    ...mapState({
      city:'city'
    }),
    ...mapGetters({
      docubleCity:'docubleCity'
    })
  },
  methods:{
    ...mapMutations(['changeCity'])
  },
  mounted(){
    this.changeCity('贵州')
  }
};
</script>
````

关于解构： data状态解构在计算属性中解构；  方法在methods中解构。

## 5  页面中访问vuex 的stats

````javascript
 每个页面都注入了vuex , $strore 中可以使用。 本组件中，使用计算属性，快捷，不消耗性能。由于vuex的状态是响应式的，vuex 变化， count也会变化。
*console*.log(this.$store.state.num);

import store from 'store';
const Counter = {
  template: `<div>{{ count }}</div>`,
  computed: {
    count () {
      // 获取store中的状态
      return store.state.count;
    }
  }
}
这样，组件中的状态就与store中的状态关联起来了。每当store.state.count发生变化时，都会重新求取计算属性，从而更新DOM。
````



![1596284193517](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1596284193517.png)



## 6  vuex中的 辅助函数

state       mapState

getters     mapGetters

mutations    mapMutations

### 6.1  State 与 mapState

当一个组件获取多种状态的时候，则在计算属性中要写多个函数。为了方便，可以使用mapState辅助函数来帮我们生成计算属性。

````javascript
 computed:{
    // 引入方式，以下两种皆可
    // 1.数组方式：
    // ...mapState(['city']),
    // ...mapGetters(['docubleCity'])
    
    // 2.对象方式：
    ...mapState({
      city:'city'
    })
 
  },
````

### 6.2  getters    与 mapGetters

有时候我们需要从 store 中的 state 中派生出一些状态，例如对列表进行过滤并计数。此时可以用到getters，getters可以看作是store的计算属性，其参数为state。

vuex 中

```
const store = new Vuex.Store({
  state: {
    todos: [
      {id: 1, text: 'reading', done: true},
      {id: 2, text: 'playBastketball', done: false}
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done);  //  filter属性，返回为true的项。
    }
  }
});
```

组件中使用

###  获取getters里面的状态，方法一

```
store.getters.doneTodos //  [{ id: 1, text: 'reading', done: true }]
//在组件中，则要写在计算属性中，
computed: {
  doneTodos () {
    return this.$store.getters.doneTodos;
  }
}
```

###  使用mapGetters获取getters里面的状态：方法二

```
import {mapState, mapGetters} from 'vuex';
computed: {
...mapState(['increment']),
...mapGetters(['doneTodos'])
}
```

## 6.3 mutations

mutations里面是如何更改state中状态的逻辑。更改Vuex中的state的唯一方法是，提交mutation，即store.commit(‘increment’)。

### 提交载荷(payload)

提交载荷就是  可以向commit传入额外的参数，即mutation的载荷。

```
vuex 中
mutations: {
  increment(state, n){
    state.count += n;
  }
}

组件中
 mounted() {
    this.$store.commit('increment', 10);
  },
```

payload还可以是一个对象。

```
mutations: {
  increment(state, payload)
  state.count += payload.amount;
}
}
store.commit('increment', {amount: 10});
```

还可以使用type属性来提交mutation。

```
store.commit({
  type: 'increment',
  amount: 10
});
// mutations保持不变
mutations: {
  increment(state, payload){
    state.count += payload.amount;
  }
}
```

注意：mutation必须是同步函数，不能是异步的，这是为了调试的方便。

### 那么，组件中，如何配置调用

那么mutation应该在哪里提交呢？ 因为js是基于事件驱动的，所以改变状态的逻辑肯定是由事件来驱动的，所以store.commit(‘increment’)是在组件的methods中来执行的。

方法1: 在组件的methods中提交

```
methods: {
  increment(){
    this.$store.commit('increment');
  }
}
```

方法2: 使用mapMutaions

用 mapMutations 辅助函数将组件中的 methods 映射为 store.commit 调用。

```
import { mapMutaions } from 'vuex';
export default {
  methods: {
    ...mapMutaions([
    'increment' // 映射 this.increment() 为 this.$store.commit('increment')
  ]),
  ...mapMutaions([
      add: 'increment' // 映射 this.add() 为 this.$store.commit('increment')
    ])
    }
}

// 因为mutation相当于一个method，所以在组件中，可以这样来使用
<button @click="increment">+</button>
```

## 6.4  actions 异步事件   dispatch方法

因为mutations中只能是同步操作，但是在实际的项目中，会有异步操作，那么actions就是为了异步操作而设置的。这样，就变成了在action中去提交mutation，然后在组件的methods中去提交action。只是提交actions的时候使用的是dispatch函数，而mutations则是用commit函数。

vuex

````javascript
  mutations: {
        increment(state) {
            state.count++;
        }

    },
    actions: {
        increment(context) {
                           console.log(context); //看注释
            context.commit('increment');
        }
    },
````

```
// action函数接受一个context参数，这个context具有与store实例相同的方法和属性。
```

![1596298793567](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1596298793567.png)

### 组件中触发方法

第一种

````javascript
 this.$store.dispatch('increment');  
````

总结： mutations 同步方法的触发， 不管是组件中，还是action异步在vuex中执行，都遵行commit 触发。

第二种

方法2: 使用mapActions，跟mapMutations是类似的。

(测试成功   原因是：import { mapState,mapGetters,mapMutations ,mapActions} from "vuex"      先引入方法)

````javascript
import { mapActions } from 'vuex'
export default {
  // ...
  methods: {
    ...mapActions([
    'increment' // 映射 this.increment() 为 this.$store.dispatch('increment')
  ]),
  ...mapActions({
  add: 'increment' // 映射 this.add() 为 this.$store.dispatch('increment')
})
}
}

// 同样在组件中，可以这样来使用
<button @click="increment">+</button>
````



## **vuex action和mutations的区别**

action的功能和mutation是类似的，都是去变更store里的state，不过action和mutation有两点不同：

1、action主要处理的是异步的操作，mutation必须同步执行，而action就不受这样的限制，也就是说action中我们既可以处理同步，也可以处理异步的操作

2、action改变状态，最后是通过提交mutation



## 6.5 组合actions

因为action是异步的，那么我们需要知道这个异步函数什么时候结束，以及等到其执行后，会利用某个action的结果。这个可以使用promise来实现。在一个action中返回一个promise，然后使用then()回调函数来处理这个action返回的结果。

vuex

````javascript
  actions:{     
    actionA(context){
        return new Promise((resolve, reject) => {
          setTimeout(() => {
            context.commit('increment');
            resolve();
          },2000);
        })
      }

   },
````

组件调用

````javascript
  methods: {
    increment() {
      this.$store.dispatch("actionA").then(() => {
        alert(0);
      });
    },
  },
````

# 6.6 mudules

module是为了将store拆分后的一个个小模块，这么做的目的是因为当store很大的时候，分成模块的话，方便管理。

每个module拥有自己的state, getters, mutation, action

````javascript
const moduleA = {
    state: {...},
    getters: {...},
    mutations: {....},
  actions: {...}
}

const moduleB = {
    state: {...},
    getters: {...},
    mutations: {....},
  actions: {...}
}

              
const store = new Vuex.Store({  //模块注册
  modules: {
    a: moduleA,
    b: moduleB
  }
});

store.state.a // 获取moduleA的状态
store.state.b // 获取moduleB的状态
````

## 模块内部的状态

对于模块内部的mutation和getter，接受的第一个参数是模块的局部状态state。顺便说一下，根结点的状态为rootState。

````javascript
const moduleA = {
  state: { count: 0},
  getters: {
    doubleCount(state){
      return state.count * 2;
    }
  },
  mutations: {
    increment(state){
      state.count ++ ;
    }
  },
  actions: {...}
}
````

## 模块的动态注册

在模块创建之后，可以使用store.registerModule方法来注册模块。

```
store.registerModule('myModule', {
  // ...
});
```

依然的，可以通过store.state.myModule来获取模块的状态。

可以使用store.unregisterModule(moduleName)来动态的卸载模块，但是这种方法对于静态模块是无效的（即在创建store时声明的模块）。

# 含有vuex的项目的结构

##  应该遵循的规则

- \1. 应用层级的状态都应该集中在store中
- \2. 提交 mutation 是更改状态state的唯一方式，并且这个过程是同步的。
- \3. 异步的操作应该都放在action里面



# 补充：

### 1. 什么是函数式组件

**函数式组件在React社区很流行使用，那么在vue里面我们要怎么用呢**

下面会涉及到的知识点： 高阶函数、状态、实例、vue组件

### 什么是函数式组件

我们可以把函数式组件想像成组件里的一个函数，入参是渲染上下文(render context)，返回值是渲染好的HTML

对于函数式组件，可以这样定义：

- Stateless(无状态)：组件自身是没有状态的
- Instanceless(无实例)：组件自身没有实例，也就是没有this

由于函数式组件拥有的这两个特性，我们就可以把它用作高阶组件(High order components)，所谓高阶，就是可以生成其它组件的组件。就像日本的高精度的母机。

### 那创造一个函数式组件吧

`functional: true`加上`render function`，就是一个最简单的函数式组件啦，show your the code, 下面就创建一个名为`FunctionButton.js`的函数式组件

```
export default {
    name: 'functional-button',
    functional: true,
    render(createElement, context) {
        return createElement('button', 'click me')
    }
}
```

提示：函数式组件比普通组件性能更好，缺点是定义的数据没有响应式。

## 2. vue首页加载慢的问题：

https://www.cnblogs.com/zyulike/p/11190012.html

### 解决方案一

1，去掉编译文件中map文件。在编译好后，我们会看到文件夹下有特别多的.map文件，这些文件主要是帮助我们线上调试代码，查看样式。所以为了避免部署包过大，通常都不生成这些文件。

在 config/index.js 文件中将productionSourceMap 的值设置为false. 再次打包就可以看到项目文件中已经没有map文件 （文件大小 35MB-->10.5MB）

2，vue-router 路由懒加载

懒加载即组件的延迟加载，通常vue的页面在运行后进入都会有一个默认的页面，而其他页面只有在点击后才需要加载出来。使用懒加载可以将页面中的资源划分为多份，从而减少第一次加载的时候耗时。



### 解决方案二

使用CDN减小代码体积加快请求速度

### 1. 为什么使用CDN

使用CDN主要解决两个问题：

1. 打包时间太长、打包后代码体积太大，请求慢
2. 服务器网络不稳带宽不高，使用cdn可以回避服务器带宽问题

### 2. 具体步骤

1.在`/index.html`中引入CDN

2.修改/build/webpack.base.conf.js中修改配置。给module.exports添加externals属性(详见https://webpack.docschina.org/configuration/externals/)，其中键是项目中引用的，值是所引用资源的名字。需要注意的是资源名需要查看所引用的JS源码，查看其中的全局变量是什么，例如element-ui的全局变量就说ELEMENT

3.删除原先的`import`

如果不删除原先的`import`，项目还是会从`node_modules`中引入资源。
也就是说不删的话，`npm run build`时候仍会将引用的资源一起打包，生成文件会大不少。所以我认为还是删了好。



## 二次 补充：

### 1 页面中放置三块路由，显示。 不是router-link

### 2 父组件调用子组件的方法：

关键词：    <child ref="mychild"></child>

**示例：**

　　**子组件：**

```
<template>
  <div>
    child
  </div>
</template>
 
<script>
  export default {
    name: "child",
    props: "someprops",
    methods: {
      parentHandleclick(e) {
        console.log(e)
      }
    }
  }
</script>
```

**父组件：**

```
<template>
  <div>
    <button @click="clickParent">点击</button>
    <child ref="mychild"></child>
  </div>
</template>
 
<script>
  import Child from './child';
  export default {
    name: "parent",
    components: {
      child: Child
    },
    methods: {
      clickParent() {
        this.$refs.mychild.parentHandleclick("嘿嘿嘿");
      }
    }
  }
</script>
```

**注意：**

　　　1、在子组件中：<div></div>是必须要存在的 ，  就是组件最外层盒子。

　　2、在父组件中：首先要引入子组件 import Child from './child';

　　  3、 <child ref="mychild"></child>是在父组件中为子组件添加一个占位，用于放置子组件方法的容器， ref="mychild"是子组件在父组件中的名字

　　  4、父组件中 components: {　　是声明子组件在父组件中的名字 }  父组件引入注册

​       5、*在父组件的方法中调用子组件的方法，很重要*   this.$refs.mychild.parentHandleclick("嘿嘿嘿");

​    方法放置在this.$refs   下面



### 3 [子组件调用父组件的方法](https://www.cnblogs.com/jin-zhe/p/9523782.html)



#### 第一种方法

是直接在子组件中通过this.$parent.event来调用父组件的方法

父

```
methods: {
    clickParent(){
    
     console.log('我是父组件的方法');
      }
  },
```

子

```
    methods: {

        parentHandleclick(e) {
        this.$parent.clickParent()
   
      }

    }
```

解析： 父组件只要使用了子组件，那么在子组件中this.$parent 中，可以拿到父组件的事件。



#### 第二种方法

是在子组件里用`$emit`向父组件触发一个事件，父组件监听这个事件就行了。

和传值一样， 子组件触发注册事件，父组件的方法是自动执行。

## 4  vue 路由经典布局  （命名路由） 

第一步： 先在路由规则中，让指定路径匹配多个组件。

```
export default new Router({
  routes: [
    {
      path: '/',
      // name: 'HelloWorld',
      components:{  <  ------------------注意点： 这里变成了复数 加s -----------
        'default': HelloWorld,
        'main': ceshi
      }
    }
  ]
})
```

第二步：

在app中 命名显示路由

```
  <div id="app">
    <div class="top">
      <router-view name="main"></router-view>
    </div>

    <div class="main">
      <router-view name="default"></router-view>
    </div>
  </div>
```

注意点： components 复数了。



使用第三方插件：

swiper 开源、免费、强大的触摸滑动插件

swiper 是纯javascript打造的滑动特效插件，面向手机、平板电脑等移动终端

Swiper 能实现触屏焦点图、触屏Tab切换、触屏轮播图切换等常用效果

https://swiperjs.com/vue