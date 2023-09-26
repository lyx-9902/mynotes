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

