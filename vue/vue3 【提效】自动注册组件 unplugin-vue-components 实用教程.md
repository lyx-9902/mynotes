# vue3 【提效】自动注册组件 unplugin-vue-components 实用教程

**Vue的按需组件自动导入。**
特点
**同时支持Vue 2和Vue 3的开箱即用。**
**同时支持组件和指令。**
支持vite,web pack,rsp ack,vue cli，汇总，esbuild和更多，由unplugin提供支持。
*Tree-SHAkable，只注册您使用的组件。
文件夹名称作为命名空间。
完整的TypeScript支持。
为流行的UI库内置解析器。
完美地与非插件图标。



还在为每次都要导入组件而烦恼吗 ？

```
// 每次都需手动导入组件
import webName from '@/components/webName.vue'

```

用 unplugin-[vue](https://so.csdn.net/so/search?q=vue&spm=1001.2101.3001.7020)-components 来帮你吧，以后组件直接拿来用即可，无需再导入啦 ！

```
<webName />

```

## 使用流程

### 1. 安装 unplugin-vue-components

```
npm i -D unplugin-vue-components
```

### 2. vite 配置中导入

vite.config.ts

```
import Components from 'unplugin-vue-components/vite'
```

plugins 中加入 Components

```
Components({}),
```

### 3. 新建组件

src/components 中的 vue 文件，会被自动注册！

新建 src/components/webName.vue

```
<template>
  <div>网站的名称</div>
</template>
```

### 4. 使用组件

src/views/test.vue

```
<template>
  <webName />
</template>

```

### 5. 重启项目

会重新生成 components.d.ts 文件（内部可见自动导入的组件）

```vue
WebName: typeof import('./src/components/webName.vue')['default']
```

访问页面正常渲染无报错，恭喜配置成功！

https://blog.csdn.net/weixin_41192489/article/details/140019854