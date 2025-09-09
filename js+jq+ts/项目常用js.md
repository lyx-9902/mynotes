# 常用记录

迭代Map对象

使用jsnewmap()函数创建的Map对象可以通过for-of循环进行迭代。

下面是一个简单的例子，通过for-of循环遍历Map对象中的所有键值对：

```
let map = new Map();
map.set('key1', 'value1');
map.set('key2', 'value2');
map.set('key3', 'value3');

for(let [key, value] of map) {
  console.log(key + " " + value);
}
```

输出结果为：

key1 value1 key2 value2 key3 value3



## 项目中的知识点记录

### 01 浏览器中不能粘贴文本

2警告:不要将您不理解或没有自己检查过的代码粘贴到DevTools控制台中。这可能会让攻击者窃取您的身份或控制您的计算机。请在下面键入“允许粘贴”以允许粘贴。

https://blog.csdn.net/weixin_54048131/article/details/135577937

控制台执行： 

allow pasting

就行了

### 02 浅说一下 import.meta.glob()

[详解](https://blog.csdn.net/pig_ning/article/details/133856944)

`import.meta.glob()` 是一个 ES 模块的特殊属性，用于动态导入多个模块，`import.meta.glob()` 方法接受一个`模式字符串`作为参数，并返回一个`Promise`，该Promise 析为一个对象，该对象包含匹配该模式的所有模块的[键值对](https://so.csdn.net/so/search?q=键值对&spm=1001.2101.3001.7020)。使用 `import.meta.glob()` 可以方便地批量导入模块，而不需要手动一个一个地导入。
这在一些需要动态加载模块的场景下非常有用，例如在构建工具中自动加载插件、动态加载路由等。



`import.meta.glob` 是一个 [Vite](https://so.csdn.net/so/search?q=Vite&spm=1001.2101.3001.7020) 特有的功能，它允许你在模块内部匹配多个模块，基于文件系统的模式。

```vue
const modules = import.meta.glob('./../../views/**/*.vue') //

export const loadView = (view) => {
  let res;
  for (const path in modules) {
    const dir = path.split('views/')[1].split('.vue')[0];
    if (dir === view) {
      res = () => modules[path]();//获取组件实例
    }
  }
  return res;
}
```







## 配置环境报错4048

https://blog.csdn.net/baixue0111/article/details/131370787

原因是：操作权限问题

解决方法：

\1. 可以在开始菜单输入栏中输入cmd，在【[命令提示符](https://so.csdn.net/so/search?q=命令提示符&spm=1001.2101.3001.7020)】右键【以管理员身份运行】，打开之后再次输入 npm install 即可。







### 词云插件

官网： https://www.goat1000.com/tagcanvas.php

