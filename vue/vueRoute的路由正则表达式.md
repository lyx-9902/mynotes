# vueRoute的路由正则表达式

Vue Router中的路由正则表达式与JavaScript的[正则表达式语法](https://so.csdn.net/so/search?q=正则表达式语法&spm=1001.2101.3001.7020)相同，可以使用常见的正则表达式语法，例如字符类、重复和分组等。
以下是一些常见的正则表达式示例：

```js
path: '/user/:id(\\d+)'
```

这可以匹配一个或多个数字。

匹配字母：

```
path: '/user/:name([a-zA-Z]+)'
```

这可以匹配一个或多个字母（不区分大小写）。

匹配字母和数字：

```
path: '/user/:id([a-zA-Z0-9]+)'
```

这可以匹配一个或多个字母或数字（不区分大小写）。

匹配具有特定格式的日期：

```
path: '/post/:date(\\d{4}-\\d{2}-\\d{2})'

```

这可以匹配 yyyy-mm-dd 格式的日期。

匹配带有可选参数的路由：

```
path: '/user/:id?'
```

这可以匹配可选参数 id，也可以匹配不带参数的路由。
注意，在Vue Router中使用正则表达式时，需要将正则表达式包含在圆括号中，并在圆括号之前使用一个冒号来指定参数名称。
另外，使用的正则表达式可能会影响路由匹配的性能。因此，应该尽量避免使用非常复杂的正则表达式。



## 项目案例

```js
  {
    path: "/system/dict-data",
    component: Layout,
    hidden: true,
    permissions: ["system:dict:list"],
    children: [
      {
        path: "index/:dictId(\\d+)",
        component: () => import("@/views/system/dict/data"),
        name: "Data",
        meta: { title: "字典数据", activeMenu: "/system/dict" },
      },
    ],
  },
```

