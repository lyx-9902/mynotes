# vue3

https://cn.vuejs.org/

https://v3.cn.vuejs.org/  这两个是同一个网站

---



这个是vue2

https://v2.cn.vuejs.org/  

 Vue 2 已经终止支持且不再维护。 [请升级到 Vue 3](https://cn.vuejs.org/) 或了解有关 [Vue 2 终止支持 (EOL)](https://v2.cn.vuejs.org/eol/) 的信息。

# 引言

**问题的起源**
vue3.0 开始 Proxy代替Object.defineProperty，产生了一些列疑惑。

- Proxy是什么？
- Proxy能干什么？
- Vue用Object.defineProperty干了什么？
- 为什么用Proxy代替Object.defineProperty？

补充知识点：

Proxy： Vue3中的响应式数据是通过ES6的Proxy来实现的。那么什么是Proxy。

MDN定义：Proxy 对象用于定义基本操作的自定义行为（如属性查找，赋值，枚举，函数调用等）。

通俗的讲Proxy是一个对象操作的拦截器，拦截对目标对象的操作，进行一些自定义的行为，一种分层的思想有点类似。

案例：

```
let target = {};
let p = new Proxy(target, {});

p.a = 37;   // 操作转发到目标

console.log(target.a);    // 37. 操作已经被正确地转发
（可以看到，通过操作p，修改了target对象的数据。）

```

[参考](https://blog.csdn.net/sj15942331889/article/details/100210046?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522163186967516780262520842%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=163186967516780262520842&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-100210046.first_rank_v2_pc_rank_v29&utm_term=Proxy&spm=1018.2226.3001.4187)



###  process

webpack是npm生态中的一个模块，依赖于node的环境，没有node是不能打包的，所以搭建项目是得npm install。process.env就是Nodejs提供的一个API，它返回一个包含用户环境信息的对象。如果我们给Nodejs 设置一个环境变量，并把它挂载在 `process.env` 返回的对象上，便可以在代码中进行相应的环境判断。

### process.env

`env` [](http://url.nodejs.cn/jzn6Ao) 包含要检查的环境变量的对象。 这使得模拟特定终端的使用成为可能。 默认值: `process.env`。

process.env属性返回一个对象，包含了当前Shell的所有环境变量。比如：process.env.NODE_ENV

名称内容是可以修改的。如果需要，你也可以把它定义为 NODE_abc或者xxx都行。

### 官方api：

https://vue3js.cn/docs/zh/guide/migration/introduction.html

使用ts重构底层代码，并对渲染打包进行逻辑速度提升。并增加了新的api方法，在项目代码上，有了更好的阅读和编写体验。

###  diff 算法 静态提升和监听缓存

vue2 是全量对比，每次编译都是逐个对比，耗时较大，vue3，改进了方法，对可能改变的dom，进行标记，准对性对比。

缓存部分： 对于复用的dom，使用缓存。不在重新编译。



# 1 项目建立

安装：

1. 在页面上以 [CDN package](https://vue3js.cn/docs/zh/guide/installation.html#cdn) 的形式导入。

2. 使用 [npm](https://vue3js.cn/docs/zh/guide/installation.html#npm) 安装它。

3. 使用官方的 [CLI](https://vue3js.cn/docs/zh/guide/installation.html#cli) 来构建一个项目，它为现代前端工作流程提供了功能齐备的构建设置 (例如，热重载、保存时的提示等等)。

   ##  npm方式

    

   ```
    npm install vue@next
      执行后，当前文件夹出现
      node_moudules
      package.json
      package-lock.json  三个文件
   ```

   

项目建立有多种方法，以下是vue/cli

## 准备工作：

对于 Vue 3，你应该使用 `npm` 上可用的 Vue CLI v4.5 作为 `@vue/cli@next`。要升级，你应该需要全局重新安装最新版本的 `@vue/cli`：

vue3依赖于Vue CLI v4.5，    Vue CLI 依赖于npm ; 所以需要npm 升级，vueCli 卸载旧版本，安装新版本，然后在通过快捷构建项目vue3的指令。

（webpack和vue-cli：Webpack 是一个前端资源的打包工具，它可以将js、image、css等资源当成一个模块进行打包。一个快速搭建vue项目的脚手架：vue-cli，使用它能快速的构建一个web工程模板）

```
 node -v  （检查一下 版本） node -v  10以上 
```

#### vue-cli安装

```
npm install vue-cli -g
```

#### vue-cli的版本查看

```
vue -V
```

#### 安装  脚手架 Vue CLI v4.5

注意点：cli目前三个版本，注意区分。安装方式分别为：

#### 如果指令不成功的处理方法

第一种：

npm install -g @vue/cli --registry=http://registry.npm.taobao.org

第二种：

C:\Users\空你吉瓦\AppData\Roaming\npm\node_modules\  删除掉npm安装包。重新初始化

##### vue CLI2

```
1. npm install vue-cli -g

2. npm uninstall vue-cli -g（如果不成功，使用cpm淘宝镜像+c）
3. 创建项目模板指令： vue init webpack project2
模板结构：
--build
    |---webpack.base.conf.js
    |---build.js等等
--config   
    |---dev.env.js
    |---prod.env.js
--src
...
```

##### vue CLI3

注意点： 百度上查得，CLI3和CLI4的区别，只是-g的位置不同，但是安装之后任然是4.  解决方式是：指定版本号

```
# 安装
1. npm install -g @vue/cli（如果不成功，使用cpm淘宝镜像）
# 查看已安装版本
vue --version 或者 vue -V

# 卸载
2. npm uninstall -g @vue/cli 
3. 创建项目模板指令：
 vue create my-project

指定版本号安装方式：
npm install -g @vue/cli@3.11.0  
npm install -g @vue/cli@3.12.1
（未解决问题：安装报错）
```

##### vue CLI4

```
先卸载，再安装
# 安装
1. npm install @vue/cli -g （如果不成功，使用cpm淘宝镜像）
vue -V 查看安装的版本
PS D:\vue3demo> vue -V
@vue/cli 4.5.13
# 卸载
2. npm uninstall @vue/cli -g
3. 创建项目模板指令：
 vue create my-project
 
模板结构：
--bublic
    |---favicon.ico
    |---index.html
--src
...
vue2 模板main.js文件

import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
}).$mount('#app')

vue3 模板main.js文件
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
```



##### vue CLI5

```bash
先卸载，再安装
npm install -g @vue/cli@next


@vue/cli 5.0.0-beta.3
卸载指令
 npm uninstall -g @vue/cli 5.0.0-beta.3
(卸载时需要区分当时安装的是全局还是项目)
模板结构：
--bublic
    |---favicon.ico
    |---index.html
--src
...
**main.js
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
```

安装完成后，可以创建项目：

```
vue create 项目名称   //回车    一步步操作下去
```



使用路由

(注意：插件和vue2的是不一样的)

```
npm install vue-router@4.0.0-beta.13

```

router.js稍作改造

```
import Vue from 'vue'

import { createRouter, createWebHistory } from 'vue-router'

const routerHistory = createWebHistory() //

import test from '@/views/test.vue'

export default createRouter({
  history: routerHistory,
  routes: [
    {
      path: '/',
      name: 'test',
      component: test
    }
  ]
})

```

main.js稍作改造

```
import { createApp } from 'vue';
import App from './App.vue'

import router from './router'

createApp(App).use(router).mount('#app')
```

app组件放置 组件视口标签

```
<router-view></router-view>
```



# 2 开发业务组件- 组合api

新增api

setup(){  数据data,和 methods方法  }   入口函数

ref  数据双向绑定的方法

let num = ref(0);  定义data

```vue
<template>
  <div>
    <h1>标题</h1>
    {{ num }}
    <button @click="myFn">按钮</button>
  </div>
</template>
<script>
import {ref} from "vue";
export default {
  name: "test",
  //  setup函数是组合api的入口函数
  setup() {
    // let conunt = 0;  //不会监听变化
    //  定义了一个名称叫做count变量，这个变量的初始值是0
    //  这个变量发生改变之后，vue会自动更新ui
    let num = ref(0);  //  数据双向绑定的方法 自动更新性能ui  注意点：包装后的值，是个对象  自动加上 .value
    // 在组合AP中，如果像定义方法，不用定义到methods中，直接定义即可
    function myFn() {
      num.value+= 1
    };
    // 注意点： 在组合API中定义的变量/方法，要想在外界使用，必须同步return {xxx,xxx} 暴漏出去
    return {num,myFn}
  },
};
</script>

<style scoped>
</style>

```

### 监听复杂数据api

```vue
<template>
  <div>
    <h1>标题</h1>
  <li v-for="(itme,index) in state.stus" :key="index" @click="remStu(index)">{{ itme.name}}</li>
    <button @click="myFn">按钮</button>
  </div>
</template>
<script>
import { reactive } from "vue";
export default {
  name: "test",
  setup() {
    // ref函数，只能监听简单类型的变化，不能监听复杂类型的变化（对象/数组）
    // 引入reactive 方法
    let state = reactive({
      stus: [
        { id: 1, name: "张三", age: 10 },
        { id: 1, name: "李四", age: 10 },
        { id: 1, name: "王五", age: 10 },
      ],
    });
    function remStu(index){
      state.stus = state.stus.filter((stu,idx) => idx !== index)
    }
    return {state,remStu}
  },
};
</script>

<style scoped>
</style>

```

##  优雅使用setup

   作用：将同一个功能涉及的数据，方法，放置放到一个模块中。方便代码的识读。

```vue
<template>
  <div>
  </div>
</template>

import { reactive } from "vue";
export default {
  name: "test",
  setup() {
  let {state,remStu} = useRemoveStudent();
    return {state,remStu}
  },
};

function useRemoveStudent(){
    let state = reactive({
      stus: [
        { id: 1, name: "张三", age: 10 },
        { id: 1, name: "李四", age: 10 },
        { id: 1, name: "王五", age: 10 },
      ],
    });
    function remStu(index){
      state.stus = state.stus.filter((stu,idx) => idx !== index)
    }
    return {state, remStu}
}

</script>
```



# Vue3.0新增特性

1. 性能比Vue2.x快1.2倍
2. 加入了按需导入按需编译，体积相比Vue2.X变小           ref 变量  使用那个引用那个 ，差别化引入。
3. 组合API
4. 更好的TypeScript支持
5. 暴露了自定义渲染的API
6. 更先进的组件

## 1 dif算法

7. 相比vue2的diff算法全层比较更新视图，vue3会在创建DOM树的内容会不会发生变化，添加一个静态标记当数据更新时生成新的虚拟DOM，对有静态标记的地方进行更新

## 2. 静态提升和缓存机制

```
8. 静态提升

9. 对比vue2vue3会复用已有的元素，哪里需要哪里调用，不需要参与更新的元素放到外面，只创建一次，在渲染时直接复用即可

10. 事件帧听器缓存

11. 默认情况下onClick会被视为动态绑定，所以每次都会去追踪他的变化，但是应为是同一个函数，所以没有追踪变化，直接缓存起来复用即可
```

## 3. Vue3.0项目创建

```
1. 创建方式 1-Vue-Cli，2-Wenpack,3-Vite(Vue新增，Vite是作者开发的一款意图取代webpack的工具，其实现原理就是利用ES6的import会去发送加载请求文件的特性，拦截这些请求，做一些预编译)

2. 安装Vite npm install -g create-vite-app
```



## 4. 组合API 

```
1. 提供了setup函数，setup函数是组合API的入口函数，
在此函数中定义变量需要通过
import引入import {ref} from 'vue'
在申明变量时let a = ref(0)当变量发送改变时，Vue会自动更新UI(ref函数注意点ref函数只能监听简单的数据类型变化，不能监听复杂的数据类型变化（对象/数组）),如果想监听复杂数据类型Vue3.0提供了一个
import {reacive} from ‘Vue’
的方法

2. 在组合API中，如果想定义方法，不用到methods中，直接在setup中定义即可

3. 注意：在组合API中定义变量或者方法，要想在外界使用，必须通过return{xxx,xxxx}的方式暴露出去

4. 组合API就是将我们封装好的具备独立共用的函数组合在一起就是组合API
```



```
 setup () {
   1.  ref函数只能监听简单的数据类型变化
   const isopen = ref(true)
   const currentId = ref(0)
   const voiceShow = ref(false)
  2.复杂数据
       const cameraInfo = reactive({
          list: [],
          camreaNum: 0
        })
        声明一个空对象
   原来
        data(){
        return {
               paramObj:{}
        }}
    现在
   let paramObj = reactive({})
   
   
使用方法
 function clickHandle(){
   currentId.value = 88   
 }
   
```



## 5. sutup函数执行时机和注意点

```
1. setup执行时机 beforeCreate > setup > Create

2. 在执行setup函数时还没有执行Createed生命周期函数，所以在setup中无法使用data和methods的，Vue为了避免错误使用，它直接将setup函数中的this修改成了undefined，setup函数只能是同步，不可以是异步
```

## 6. reactive

```
1. reactive是Vue3中提供的实现响应式数据的方法，Vue3中的响应式数据是通过ES6的Proxy来实现的

2. reactive参数必须是对象（json/arr）如果reactive传递了其他对象，默认情况下修改对象，界面不会自动更新，如果想更新，可以通过重新赋值的方式
```



## 7. ref

```
1. ref和reactive一样，也是用来实现响应式数据的方法，但是reactive必须传递一个对象，所以在企业开发中如果我们想让某个变量实现响应式的时候会非常麻烦，所以Vue3 就提供了ref方法，实现对简单数据的监听

2. ref的本质其实还是reactive，系统会自动更具我们给ref传入的值将他装换成reactive（{value：xx}）

3. ref 注意点：在Vue中使用ref的值不用通过Value来获取，在JS中使用ref的值必须通过Value来获取
```



```vue

<template>
  <div class="home">
    home页面9 <br>
    <button @click="test">修改</button>
    {{ list }}
  </div>
</template>

<script setup>

import { ref, reactive } from "vue"

const message = ref("11")
const list = reactive({
  data:[12]
})

const test = () => {

  message.value = 99;  //使用简单变量

  list.data = [111,22,33]  //使用复杂变量

}

</script>

<style scoped></style>
```







## 8. ref和reactive的区别

```
1. 如果在template中使用的是ref的数据类型，那么Vue会自动帮我们添加.value

2. 如果在template中使用的是reactive类型的数据，那么Vue不会自动帮我们添加.value
```

### 补充： Vue3只读代理

readonly、isReadonly、shallowReadonly

```
isRef: 检查一个值是否为一个 ref 对象

isReactive: 检查一个对象是否是由 reactive 创建的响应式代理

isReadonly: 检查一个对象是否是由 readonly 创建的只读代理

isProxy: 检查一个对象是否是由 reactive 或者 readonly 方法创建的代理

```

```
	import {ref, reactive,toRefs,readonly,isRef,isReactive,isReadonly,isProxy } from 'vue'
	export default {
		name:'App',
		setup(){
			let car = reactive({name:'奔驰',price:'40W'})
			let sum = ref(0)
			let car2 = readonly(car)
 
			console.log(isRef(sum))
			console.log(isReactive(car))
			console.log(isReadonly(car2))
			console.log(isProxy(car))
			console.log(isProxy(sum))
			
			return {...toRefs(car)}
		}
	}
```





## 9. 递归监听

```
1. 默认情况下，无论是ref还是reactive都是递归监听

2. 递归监听存在的问题，如果数据量比较大，非常消耗性能
```



## 10. 非递归监听 shallowRef/shallowReactive

```
1. 如何触发：如果是shallowRef数据类型，可以通过triggerRef来触发

2. 应用场景：只有在需要监听的数据量较大时，我们才使用shallowRef/shallowReactive
```



## 11. to-Raw

```
1. ref/reactive数据类型特点：每次修改都会被追踪，都会更新UI界面，但是非常消耗性能，所以当我们有一些操作不需要追踪，不需要更新UI界面那么这个时候，我们就可以通过toRaw方法拿到他的原始数据，对原始数据进行修改这样就不会被追踪，这样就不会更新UI界面，提高性能

2. 如果想通过toRaw拿到ref类型的原始数据（创建时传入的那个数据）那么就必须明确的告诉toRaw方法，要获取的是.value值，应为经过Vue处理之后,.value中保存的才是传入的的那个原始数据
```



## 12. toRaf

```
如果利用toRaf将某一个对象中的属性变成响应式的数据，我们修改响应式的数据是会影响到原始数据的，但是如果响应式的数据是通过toref创建的，那么修改了数据并不会触发UI界面的更新
```

————————————————
[新增新特性-参考](https://blog.csdn.net/weixin_47660582/article/details/110825193)

补充

## 13 vue中的组件通信

![通信](https://www.javascriptc.com/vue3js/images/components_provide.png)

作用：实现**祖与后代组件间**通信

祖组件中：

```
<template>
	<div class="app">
		<h3>我是App组件（爷），{{name}}--{{price}}</h3>
		<Child/>
	</div>
</template>
 
<script>
	import { reactive,toRefs,provide } from 'vue'
	import Child from './components/Father.vue'
	export default {
		name:'App',
		components:{Child},
		setup(){
			let car = reactive({name:'奔驰',price:'40W'})
			provide('car',car) //给自己的后代组件传递数据
			return {...toRefs(car)}
		}
	}
</script>
```

后代组件中：

```
<template>
	<div class="son">
		<h3>我是子组件（子），{{car.name}}--{{car.price}}</h3>
	</div>
</template>
 
<script>
	import {inject} from 'vue'
	export default {
		name:'MySon',
		setup(){
			let car = inject('car')
			return {car}
		}
	}
</script>
```





## 知识点：

1. vue3环境配置与项目升级
2. composition API
3. setup函数的使用细节
4. reactive与ref的使用与区别
5. computed的使用
6. readonly使用详解
7. watchEffect的使用详解
8. watchEffect的清除副作用（解决搜索防抖）
9. watch的使用方法
10. 声明周期钩子函数
11. 依赖注入
12. 模板Refs
13. 响应式系统工具集





## 13

# vue3中使用路由

1.    npm安装  

```
npm install vue-router@4
```

2. 新建 routes.js文件 [参考](https://blog.csdn.net/qq_39115469/article/details/113816161)

- history模式：在路由index.js文件中导入 createWebHistory

```
import { createRouter, createWebHistory } from 'vue-router'
import Home from '../views/Home.vue'
 
const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    component: () => import('../views/About.vue')
  }
]
 
const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})
 
export default router
```

- hash模式：在路由index.js文件中导入 createWebHashHistory

```
import { createRouter, createWebHashHistory } from 'vue-router'
import Home from '../views/Home.vue'
 
const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    component: () => import('../views/About.vue')
  }
]
 
const router = createRouter({
  history: createWebHashHistory(process.env.BASE_URL),
  routes
})
 
export default router
```

记得main.js中引用一下

```
import { createApp } from 'vue'
import App from './App.vue'
import router from '@/routes'


createApp(App).use(router).mount('#app')
```

或者

```
import { createApp } from 'vue'
import router from '@/router/index'   ****  
import store from '@/store'
import Vant from 'vant'
import 'vant/lib/index.css'
import App from './App.vue'

const app = createApp(App)
app.use(router)  ***
app.use(store)
app.use(Vant)
app.mount('#app')
console.log('vm', app)
```

代码中使用

```
setup (props, context) {
    const router = useRouter()
     router.push('/')

```





# $router和$route的区别

```
router为VueRouter的实例，相当于一个全局的路由器对象，里面含有很多属性和子对象，例如history对象。。。经常用的跳转链接就可以用this.$router.push，和router-link跳转一样。。。

route相当于当前正在跳转的路由对象。。可以从里面获取name,path,params,query等。。

```

# 设置项目ip

1、创建vue.config.js

(cli3相对于cli2，之前的build和config文件夹不见了，那么应该如何配置 如webpack等的配那只需要在项目的根目录下vue.config.js
文件（是根目录，不是src目录)）

[[vue-cli3.0 环境变量与模式](https://www.cnblogs.com/heroljy/p/9305263.html)](https://www.cnblogs.com/heroljy/p/9305263.html)



# Vue3 如何挂载全局方法

ue2.x挂载全局是使用`Vue.prototype.$xxxx=xxx`的形式来挂载，然后通过`this.$xxx`来获取挂载到全局的变量或者方法 。 在vue3.x这种方法显然是不行了，vue3中在setup里面我们都获取不到this，官方提供了另一种方法来让我们使用。

挂载axios 

```
import { createApp } from 'vue'
import App from './App.vue'
import router from '@/routes'
import axios from 'axios'
const app =  createApp(App) ;

/**
 * 远程请求时判断token值是否还在
 */
 axios.interceptors.request.use(
    config => {
     let token = localStorage.getItem("ZJ_T");

      if (token) {
        // 每次发送请求之前判断是否存在token，如果存在，则统一在http请求的header都加上token，不用每次请求都手动添加
        config.headers.common["X-Token"] = token;
      }
      return config;
    },
    err => {
      return Promise.reject(err);
    }
  );
  
app.config.globalProperties.$axios = axios;  // 实例上挂载axios
app.config.globalProperties.$wechat = process.env.VUE_APP_TARGET + "/wechat"; 
 app
.use(router)
.mount('#app') ;
```

# vue3引入  ElementPlus 

```
 npm install element-plus --save
```

main.js

```
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
...
app
.use(router)
app.use(ElementPlus)
.mount('#app') ;

```

npm install less less-loader --dev

## 组合式 API？

[选项式API 到组合式API变化](https://img-blog.csdnimg.cn/img_convert/89989fd368ed3cf729422fe036df86b3.gif)

![](https://img-blog.csdnimg.cn/img_convert/89989fd368ed3cf729422fe036df86b3.gif)

[响应式数据](https://blog.csdn.net/m0_61612505/article/details/124651830?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-4-124651830-blog-112979205.pc_relevant_multi_platform_whitelistv3&spm=1001.2101.3001.4242.3&utm_relevant_index=7)

痛点：一个大型组件，这种碎片化使得理解和维护复杂组件变得困难。选项的分离掩盖了潜在的逻辑问题。此外，在处理单个逻辑关注点时，我们必须不断地“跳转”相关代码的选项块。（页面的每个功能都有自己的data和methods,当功能点过多时，不免造成阅读代码块的混乱，不断地跳转。如果一个功能的data和methods放到一起，则更加方便。）那么如何设计，如下：

## setup组件选项 解析

知识背景：注意vue3新特性 7.8

#### demo1

如下是一个列表翻页的功能。

实现一个功能，常用的有： 

声明变量，和VUE中使用变量

```
 import { ref, reactive } from "vue";
 
 setup() {
    let num = ref(0);
    let nupageSizem = ref(10); // 默认每页显示的条数
    let currentPage = ref(1); // 默认显示第几页
    let total = ref(100); // 总条数

    let num1 = ref({ name: "tom" });

    let tableData = reactive({
      list: [],
      total:10  // 总条数
    });

    function searchTableData() {
      this.$axios.defaults.withCredentials = true;
      this.$axios
        .post(this.$wechat + "/rqhbibridgesurvey?pageNum=1&pageSize=10", {
          latitude: "23.129163",
          longitude: "113.264435",
          name: "",
        })
        .then((res) => {
          let datas = res.data.resultData.list;
          tableData.list = datas;
         total = res.data.resultData.total;
        })
        .catch((error) => {
          console.log(error);
        });
    }
    return { num, num1, nupageSizem, currentPage, total, tableData, searchTableData };
  },
```

 ref, reactive 用于变量声明， vue中标签需要使用的变量，需要return出去。

#### demo2

 使用钩子函数

```
<script>
    import { onMounted, reactive } from 'vue'
    import { getAboutInfo } from '@/api/setting'

export default {
  setup () {
    const data = reactive({
      about: {
        mac: ''
      }
    })
    const methods = {
      getInfo: async () => {
        const { data: res } = await getAboutInfo()
        data.about = res.data
      }
    }
    onMounted(() => {
      methods.getInfo()
    })
    return { data }
  }
}
  </script>
```



注意点：

由于在执行 `setup` 时尚未创建组件实例，因此在 `setup` 选项中没有 `this`。这意味着，除了 `props` 之外，你将无法访问组件中声明的任何属性——**本地状态**、**计算属性**或**方法**。



vue3 方法集

```
import { reactive, readonly, ref } from '@vue/reactivity'

import { onMounted } from '@vue/runtime-core'

```

