**场景应用：避免写一大堆的import，比如关于Vue和Vue Router的**

配置后： 

```
import {computed,ref } frome "vue"     这一句就省略了
```



1、 安装：

```
npm i -D unplugin-auto-import
```

2、配置vite.config

```
import AutoImport from 'unplugin-auto-import/vite'//按需自动加载API插件

引入：
AutoImport({ imports: ["vue", "vue-router"] }),
```



配置参考：

```json
import { fileURLToPath, URL } from 'node:url'
import path from "path";
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import vueJsx from '@vitejs/plugin-vue-jsx'
import vueDevTools from 'vite-plugin-vue-devtools'
      import AutoImport from 'unplugin-auto-import/vite'//按需自动加载API插件  <----- 看这里

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
        AutoImport({ imports: ["vue", "vue-router"] }),  <----- 看这里
    vueJsx()
  ],
  
  resolve: {
    alias: {
       // 设置路径
       "~": path.resolve(__dirname, "./"),
       // 设置别名
       "@": path.resolve(__dirname, "./src"),
    },
       // https://cn.vitejs.dev/config/#resolve-extensions
       extensions: [".mjs", ".js", ".ts", ".jsx", ".tsx", ".json", ".vue"],
  }
})

```

