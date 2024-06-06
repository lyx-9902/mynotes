# antDesignVue

##  图标使用

**使用注意**： 版本号。本案例为4.x  不同版本可能有不用使用方式。

语义化的矢量图形。使用图标组件，你需要安装 `@ant-design/icons-vue` 图标组件包：

第一步：引入

```
npm install --save @ant-design/icons-vue
```

第二步：使用

```vue
<template>
  <a-space>
    <HomeOutlined />
    <SettingOutlined />
    <SmileOutlined />
  </a-space>
</template>
 
<script>
import { HomeOutlined, SettingOutlined, SmileOutlined } from '@ant-design/icons-vue';
 
export default {
  components: {
    HomeOutlined,
    SettingOutlined,
    SmileOutlined
  }
};
</script>
```

在上面的例子中，我们导入了三个图标组件`HomeOutlined`、`SettingOutlined`和`SmileOutlined`，并在模板中直接使用它们。`<a-space>`是Ant Design Vue中的空间组件，用于排列图标。

**注意**：图标名称遵循`IconNameOutlined`的格式，`Outlined`表示图标的样式。Ant Design Vue 4.x同时提供填充图标（`Filled`）、双色图标（`TwoTone`）和线框图标（`Outline`），你可以根据需要导入相应的图标组件。

案例2

```vue
<smileTwoTone />

//注意：大驼峰写法
import { SmileTwoTone } from '@ant-design/icons-vue';
```

