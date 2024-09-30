

## vue3创建项目

## 补充：

**vue中的特殊标签  component** 

它允许你动态地绑定到一个组件。这意味着你可以根据某些条件或数据动态地渲染不同的组件。

`<component>` 元素有一个特殊的 `is` 属性，该属性用于指定要渲染的组件。

```

<template>  
  <div>  
    <component :is="setComponentObject"></component>  
  </div>  
</template>


import ComponentA from './ComponentA.vue';  
import ComponentB from './ComponentB.vue'; 
setComponentObject可以是组件变量， 也可以是普通的标签。例如 div  a 。为div是就是div标签，也可以是其他的HTML标签,比如input，select，img等等都可以的

```









1.vue3官网 [地址](https://cn.vuejs.org/guide/quick-start.html#creating-a-vue-application)

使用vite快速创建项目 

```
npm init vue@latest
```



```
 Project name: … <your-project-name>
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit testing? … No / Yes
✔ Add Cypress for both Unit and End-to-End testing? … No / Yes
✔ Add ESLint for code quality? … No / Yes
✔ Add Prettier for code formatting? … No / Yes

Scaffolding project in ./<your-project-name>...
Done.
```



```
 cd <your-project-name>
> npm install
> npm run dev
```

## vue3的全局变量配置

```
app.use(router)
app.use(ElementPlus)
app.mount('#app')
app.config.globalProperties.$axios = axios;  //配置axios的全局引用
```

## 使用  elementplus

```
npm install element-plus --save
```

如果你对打包后的文件大小不是很在乎，那么使用完整导入会更方便。

main.js

```vue
// main.ts
import { createApp } from 'vue'
import ElementPlus from 'element-plus'  <--
import 'element-plus/dist/index.css'  <-- 
import App from './App.vue'

const app = createApp(App)

app.use(ElementPlus)  <-- 
app.mount('#app')
```



## [vite](https://so.csdn.net/so/search?q=vite&spm=1001.2101.3001.7020)中如何使用环境变量 

[vue2](https://so.csdn.net/so/search?q=vue2&spm=1001.2101.3001.7020)中，webpack帮我们做了处理，使浏览器可以直接识别node的process.env变量，从而实现了浏览器识别环境变量的功能。

vite中，我们的代码运行在浏览器环境中，因此是无法识别**process.env**变量的。（这意味着，vite中识别环境变量的方式与webpack中不同

vite中配置如下：

我们在项目的根目录下，创建**.env**文件

```
VITE_HELLO = "小伙子，我是base数据"     注意点：变量以VITE_前缀 才能识别，设计原因是避免混淆。
```

创建 **.env.development**文件，写入测试内容；

```
VITE_HI = "小伙子，我是development数据"
```

 创建 **.env.production** 文件，写入测试内容

```
VITE_MD =  "小伙子，我是production数据"
```

main.js中使用

```
console.log(' VITE_HI: ',  import.meta.env.VITE_HI);
console.log(' VITE_HELLO: ',  import.meta.env.VITE_HELLO);
console.log(' VITE_MD: ',  import.meta.env.VITE_MD);
```

[参考](https://blog.csdn.net/weixin_46769087/article/details/128120034)



## 项目中使用elementPlus记录

[JavaScript验证密码合法性，必须包含数字字母特殊符号（用正则表达式）](javascript:void(0);)

/^(?=.*\d)(?=.*[a-zA-Z])(?=.*[@*#$%^&+=~!?]).{8,}$/*



该正则表达式的意思是：

- `^` 表示字符串的开头
- `(?=.*\d)` 表示后面必须包含至少一个数字
- `(?=.*[a-zA-Z])` 表示后面必须包含至少一个字母
- `(?=.*[@#$%^&+=~!?])` 表示后面必须包含至少一个特殊符号（这里列出了一些常见的特殊符号）
- `.{8,}` 表示后面必须至少有 8 个字符（这里可以根据需要修改）

完整的 JavaScript 代码如下：

```

function validatePassword(password) {
  var regex = /^(?=.*\d)(?=.*[a-zA-Z])(?=.*[@#$%^&+=~!?]).{8,}$/;
  return regex.test(password);
}
// 测试代码
console.log(validatePassword("abc123$%")); // true
console.log(validatePassword("abcABC123")); // false
console.log(validatePassword("P@ssword")); // false
```

注意：该正则表达式只能验证密码是否符合要求，并不能保证密码的安全性。建议在实际应用中采取更多的措施来保护密码安全。



## 使用vite + antUI+ aoios +mock 创建项目

### 🍊项目使用 mock数据

引入axios插件

```
npm install mockjs
    使用axios请求
npm install axios
```

 注意点：src下创建mock目录 根目录下实测不行。

mock下创建 index.js文件

```js
//导入Mock
import Mock from 'mockjs'

// 使用官方的数据符号
Mock.mock('/mock/data/customerName', 'get', {
    "data|10": [{
        id: '@id', //随机id
        name: '@cname', //随机名称 @name英文名称 @cname中文名称
        phone: /^1[34578]\d{9}$/, //随机电话号码
        'age|11-99': 1, //年龄  属性名(age)、生成规则(rule)、属性值(value) 'age|rule': value
        address: '@county(true)', //随机地址 @county(true)省市县  @county(false)||@county()县||区||-
        email: '@email', //随机邮箱
        isMale: '@boolean', //随机性别
        createTime: '@datetime', //创建时间 可以自定义格式 @datetime(yyyy-MM-dd hh:mm:ss)
        paragraph: '@cparagraph',
    }]
})

第二种 返回自定义的数据
Mock.mock('/mock/login', 'post', ()=>{
   return {
    "code": 200,
    "msg": "操作成功",
    "data": {
        "token": "eyJ0eXAiOiJKV1Q"
    }
   }
})
```

main.js中引入

```
import "@/mock/index.js"//引入mock接口
```



组件中测试使用

```js
import axios from 'axios';
axios.get("/mock/data/customerName").then((res)=>{
  console.log(res);  //成功返回数据
})

接下来：可以自己去封装request,使用拦截器做一些事情。
```

### 🍊pinia的数据固化

  安装使用pinia后，由于数据都是运行时产生，所以刷新时，会丢失，恢复到出示状态。

   第一种： 使用localstory 缓存，或使用插件。

   第二种： 请求接口。  可以在router.beforeEach,判断用户信息有没有恢复默认状态，有的话就重新请求一下接口。 并更新菜单数据。

### 🍊NProgress进度条

```
npm install nprogress
```

  使用

```
import NProgress from 'nprogress';
import 'nprogress/nprogress.css'; // 这是 NProgress 的默认样式

// 启动进度条
NProgress.start();

// 增加进度条（0.1 到 1.0 之间的任何值）
NProgress.set(0.4); 

// 随机增加进度条（这里使用了内部算法来确定增加的量）
NProgress.inc(); 

// 完成进度条
NProgress.done();

```

