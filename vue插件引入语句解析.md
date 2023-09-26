

# vue插件引入语句解析

第一种情况：

带有路径的标志/

```
import router from './router'
```

第二种： from后是一个字符串

main.js

```
// 案例  ElementUI
import ElementUI from 'element-ui'
Vue.use(ElementUI)
```

测试1：

把项目中node_modules中element-ui的文件夹改名，启动项目。报错

```
 ENOENT: no such file or directory, open 'D:\work\yla\node_modules\element-ui\index.js'
```

说明：import ElementUI from 'element-ui',语句首先到node_modules中去找相同名字的文件项目，并查找根目录下的index.js文件。

测试2：如果没有index.js ，会报错吗

查看node_modules中 项目引用的其他插件，发现有的根目录下没有index.js。

```
domhandler插件
--lib  (点开发现一个index.js)
--LICENSE
--package.json
--readme.md
```

