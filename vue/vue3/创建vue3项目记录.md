

## vue3创建项目

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
