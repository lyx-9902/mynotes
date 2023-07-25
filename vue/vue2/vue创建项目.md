# vue创建项目

题外补充：

```
开发依赖 ： (例如webpack工具，只是代码开发阶段时使用，项目打包后，就不需要这个了)
npm i xxxx --save-dev ; 
npm i xxxx -D ;

生产依赖： （例如axios、element-ui这种插件要在运行中使用的）
npm i xxxx --save ; 
npm i xxxx -S; 
npm i xxxx
```

附注：

vue重写push和replace方法？

重写原因：编程式导航时，点击当前所在的路由时，控制台报如下的错误信息

报错原因：“[vue-router](https://so.csdn.net/so/search?q=vue-router&spm=1001.2101.3001.7020)”: “^3.5.3”，引入了promise，再调用push或者replace方法的时候会返回一个promise对象。push和replace方法中没有处理成功和失败的1回调。

```
解决方法之一 常用
/**
 * 重写路由的push方法
 */
const routerPush = Router.prototype.push
Router.prototype.push = function push (location) {
  return routerPush.call(this, location).catch(error => error)
}
```





什么是vue-cli

　是vue官方提供的脚手架工具。脚手架工具简单讲就是自动将项目需要的环境、依赖等信息都配置好。

## 1. 创建项目



检查版本号和查看是否安装成功

```
vue-cli
```

### vue2

vue -Cli创建方式

```
npm install -g vue-cli
```

**cli2创建项目**

```
vue init webpack  "项目名称"
```

 接下来根据需求 next  ,  选择好后，npm自动下载项目基础模板。

### vue

vue -Cli创建方式

```
npm install -g @vue/cli
```

 创建项目

```
 vue create myProject
```

## 2.安装less

less安装的注意点是：webpack less  loader 版本都需要对应,否则会报错。

那么咱们不妨放弃最新版本的，安装一个低版本的less和less-loader

webpack 3.12.0  

```
npm install less-loader@4.1.0
npm install less@3.9.0
```



组件中使用：

```css
<style scoped lang="less">
h1, h2 {
  font-weight: normal;
  a {
  color: blue;
}
}
```

对于项目的通用基础样式

assets文件下，新建index.less

main.js中引入

```js
import "./assets/css/index.less"

new Vue({
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
})

```

## 3 引入element ui

npm 安装

推荐使用 npm 的方式安装，它能更好地和 [webpack](https://webpack.js.org/) 打包工具配合使用。

```shell
npm i element-ui -S
```

在 main.js 中写入以下内容：

```js
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
});
```

可以直接使用了

## 4.vuex

**一 安装        npm i vuex**

注意: 安装时不指定版本,会安装最新版本。vuex的4版本,只能在[vue3](https://so.csdn.net/so/search?q=vue3&spm=1001.2101.3001.7020)中使用,项目时vue2的要安装4版本以下的vuex版本。

```
指定版本 npm install vuex@next --save
这里
指定版本 npm install vuex@3.0.1 --save
```

关于npm命令中@next `@next`确实一般表示下一个发布的版本，但它只是一个标识。

`-S`的作用我知道，相当于`--save`

**二、**store回顾

vuex分为五个大块

state： 统一定义公共数据（类似于data(){return {a:1, b:2，xxxxxx}}）

mutations ： 使用它来修改数据(类似于methods)

getters： 类似于computed(计算属性，对现有的状态进行计算得到新的数据-------派生 )

actions： 发起异步请求（通过axios返回数据后，调用mutations来修改state数据）

modules： 模块拆分



#### state 

**在组件中**，通过`this.$store.state.属性名`来访问。

mapState 辅助函数,映射到组件的computed中

```
1.导入  
import { mapState } from "vuex"
computed:{ // 2.使用    
...mapState（['count']）
}
```

#### getters 

作用：它是 Vuex 中的计算属性，当 Store 数据源发生变化时，Getter 的返回值会自动更新。

```
new Vuex.store({
  // 省略其他...
  getters: {
    // state 就是上边定义的公共数据state
    getter的名字1: function(state) {
      return 要返回的值
    }
  }
})
```

使用格式

在组件中通过：`$store.getters.getter的名字` 来访问

第二种方式

基于 mapGetters 辅助函数，可以把 store 中的 getter 映射为当前组件的计算属性。

```
computed: { 
  ...mapGetters(['xxx']), 
  ...mapGetters({'新名字': 'xxx'})
}
```



#### mutations   

  每一项都是一个函数，可以声明两个形参  

第一个参数是必须的，表示当前的state。在使用时不需要传入 ；

第二个参数是可选的，表示载荷，是可选的。在使用时要传入的数据

```
new Vue.store({
  // 省略其他...
  mutations：{
    // 每一项都是一个函数，可以声明两个形参
    mutation名1：function(state [, 载荷]) {
  
    },
    mutation名2：function(state [, 载荷]) {
  
    }
    }
})
```

  使用格式

```
this.$store.commit('mutation名', 实参)   
```

mapMutations 辅助函数

```
组件中：  把add从vuex中映射到当前组件的methods方法
methods：{
 ...mapNutations(['add'])
}
```

#### actions 

- actions是vuex的一个配置项
- 作用：发异步请求获取数据，调用mutations来保存数据，将整个ajax操作封装到Vuex的内部
- 要点：
- - action 内部可以发异步请求操作
  - action是间接修改state的：是通过调用 mutation来修改state

**定义格式**

```
new Vuex.store({
  // 省略其他...
  actions: {
    // context对象会自动传入，它与store实例具有相同的方法和属性
    action的名字: function(context, 载荷) {
      // 1. 发异步请求, 请求数据
      
      // 2. commit调用mutation来修改数据
      
      // context.commit('mutation名', 载荷)
    }
  }
})
```

**调用格式**

1、直接使用：在组件中通过this.$store.dispatch('actions的名字', 参数)来调用action

2、还可以基于 Vuex 提供的 mapActions 辅助函数，可以方便的把 Store 中指定的 Action，映射为当前组件的 methods:

map辅助函数：

```js
methods: { ...mapActions(['actions名']), ...mapActions({'新名字': 'actions名'}) }
```

#### modules的配置

所有的全局数据、方法都集中在了一起，导致 Vuex 的结构混乱，不利于现阶段的开发和后期的维护。

所以 拆分模板，把复杂的场景按模块来拆开

```
export default new Vuex.Store({
  // state: 用来保存所有的公共数据
  state: {},
  getters: {},
  mutations: {},
  actions: {},
  modules: {
    模块名1： {
            // namespaced为true，则在使用mutations时，就必须要加上模块名
        namespaced: true, 
          state: {},
            getters: {},
            mutations: {},
            actions: {},
            modules: {}
    }，
    模块名2： {
        // namespaced不写，默认为false，则在使用mutations时，不需要加模块名
          state: {},
            getters: {},
            mutations: {},
            actions: {},
         modules: {}
    }  
  }
})
```

也可以进一步对文件进行拆分

```
|--store /
|------- index.js # 引入模块
|------- modules
|-------------- / mod1.js # 模块1
|-------------- / mod2.js # 模块2
```

访问数据和修改数据的调整

访问模块中的数据，要加上模块名

```
获取数据项：  {{$store.state.模块名.数据项名}}
获取getters： {{$store.getters['模块名/getters名']}}
复制代码
```

访问模块中的mutations/actions:

- 如果namespaced为true，则需要额外去补充模块名

- 如果namespaced为false，则不需要额外补充模块名

  ```
  $store.commit('mutations名')        // namespaced为false
  $store.commit('模块名/mutations名')  // namespaced为true
  ```

  使用了modules之后，在访问数据时就要额外添加modules的名字了。

  结论： 在使用modules时，建议都给加上namespaced!

  

————————————————
[原文链接](https://blog.csdn.net/m0_70477767/article/details/125155540)

## 5. js-cookie

```
npm install --save js-cookie

import Cookies from 'js-cookie'
```

添加cookie

```
// 创建一个名称为name，对应值为value的cookie，由于没有设置失效时间，默认失效时间为该网站关闭时
Cookies.set(name, value)

// 创建一个有效时间为7天的cookie
Cookies.set(name, value, { expires: 7 })

// 创建一个带有路径的cookie
Cookies.set(name, value, { path: '' })

// 创建一个value为对象的cookie
const obj = { name: 'ryan' }
Cookies.set('user', obj)

```

获取cookie

```
// 获取指定名称的cookie
Cookies.get(name) // value

// 获取value为对象的cookie
const obj = { name: 'ryan' }
Cookies.set('user', obj)
JSON.parse(Cookies.get('user'))

// 获取所有cookie
Cookies.get()

```

删除cookie

```
// 删除指定名称的cookie
Cookies.remove(name) // value

// 删除带有路径的cookie
Cookies.set(name, value, { path: '' })
Cookies.remove(name, { path: '' })

```

## 6. Nprogress—页面加载的虚假进度条

npm 引入

```
npm install nprogress@0.2.0   指定版本号
```

main.js中使用

```
import NProgress from "nprogress"
import "nprogress/nprogress.css"

定义
NProgress.inc(0.2)
NProgress.configure({ easing: "ease", speed: 500, showSpinner: false })
```

一般在路由中引入使用

```
router.beforeEach((to, from, next) => {  
 NProgress.start()   // 开始
......
})

router.afterEach(() => {
  NProgress.done() // 关闭
})
```

## 7 vue中的路由钩子

vue里面提供了三大类钩子，按照放置位置不同，分为

 1、全局钩子 2、某个路由的钩子 3、组件内钩子  （两种函数，实现）

在前端路由跳转中，路由跳转前都是会经过beforeEach，而beforeEach可以通过next来控制到底去哪个路由。
根据这个特性我们就可以在beforeEach中设置一些条件来控制路由的重定向。
常见的使用场景有：

1、验证用户是否登录（若未登录，且当前非登录页面，则自动重定向登录页面）；
2、用户权限；
3、用户输入的路路径是否存在，不存在的情况下如何处理，重定向到哪个页面。

### router.addRoutes方法

动态添加更多的路由规则。参数必须是一个符合 routes 选项要求的数组。

案例

场景：路由的权限验证。 如果你的网页有[普通用户，管理员.....]等多种角色类型，不同的角色能看到的页面应该是不同的

```
const router = new VueRouter([
  {
    path: '/',
    name: 'Home',
    component: Home
  }]),
  
let route=[
{
  path: '/pageA',
  name: 'pageA',
  component: pageA,
}，...
]
 自定义的过滤条件
router.addRoutes(route);
export default router
```

## 8 font-awesome在Vue项目中的使用（npm使用）

https://fontawesome.dashgame.com/

项目中element ui中的字体图标数量有限，如有需要，也可以引入其他专门的图标库。

初始化一下

```
npm i font-awesome -S
```

main.js中引入

```
import 'font-awesome/css/font-awesome.min.css'

```

在需要的vue页面中使用