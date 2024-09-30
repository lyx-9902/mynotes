## 引入 ant-design-vue [#](https://www.antdv.com/docs/vue/getting-started-cn#引入-ant-design-vue)

本案例：创建项目Vite

### 使用组件

#### 安装 [#](https://www.antdv.com/docs/vue/getting-started-cn#安装)

```
npm i --save ant-design-vue@4.2.1
```

安装图标

```
npm i @ant-design/icons-vue
```



main.js

```css
import { ConfigProvider } from "ant-design-vue";  //引入中文配置

app.use(ConfigProvider)//中文
```



PACKAGE.JSON新增记录

```
"dependencies": {

 "@ant-design/icons-vue": "^7.0.1",
 "ant-design-vue": "^4.2.1",
  "unplugin-vue-setup-extend-plus": "0.4.9",
```

