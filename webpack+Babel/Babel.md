## 使用Babel升级工具

https://blog.csdn.net/c183662101/article/details/106363055/

官方的介绍是这样的

> 一个工具，可以更新大多数使用babel的依赖关系，配置文件，和JavaScript文件(将来可能会更多)。

## 一些常识：

 npm install --save-dev @babel/preset-env  

--save-dev   指的是  安装到开发环境，   babel插件 的作用是， 你可以使用 js高级语法， 但是浏览器只能解析低版本js,  babel的作用就是 对包含包版本js的 文件， 编译成没有高版本的js文件，  所以， 如果 正式环境，不需要。



# 1. Babel 是什么

Babel 是一个 JavaScript 编译器

Babel 是一个工具链，主要用于在旧的浏览器或环境中将 ECMAScript 2015+ 代码转换为向后兼容版本的 JavaScript 代码

主要作用：

- 转换语法
- Polyfill 实现目标环境中缺少的功能 (通过 [@babel/polyfill](https://babel.docschina.org/docs/en/babel-polyfill))
- 源代码转换 (codemods)



使用方式：

preset   预设

plugins  插件

polyfil    特殊api 转义 

（ Babel默认只转换新的JavaScript语法（syntax），如箭头函数等，而不转换新的API，比如Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise等全局对象，以及一些定义在全局对象上的方法（比如Object.assign）都不会转码；因此我们需要polyfill；）



### CLI 命令行工具

[@babel/cli](https://www.babeljs.cn/docs/babel-cli) 是一个能够从终端（命令行）使用的工具。下面是其安装命令和基本用法：

```
npm install --save-dev @babel/core @babel/cli

./node_modules/.bin/babel src --out-dir lib
```



### 2 实操命令

### 1  npm init

###  2  安装 插件

 cnpm install --save-dev @babel/core @babel/cli      （@babel/core  核心插件  ；@babel/cli  命令行工具，作用是，可以在命令行中，执行编译）

新建.babelrc 配置文件

###  3   插件和预设（preset）

案例：

 

```javascript
npm install --save-dev @babel/plugin-transform-arrow-functions  ( es6的箭头函数，转换为es5)

使用： 

./node_modules/.bin/babel src --out-dir lib --plugins=@babel/plugin-transform-arrow-functions

 注意点： 斜杠，使用  \

.\node_modules\.bin/babel src --out-dir lib --plugins=@babel/plugin-transform-arrow-functions

  （babelrc  配置文件，暂时不用），执行编译， 成功。
```

这是个好的开始！但是我们的代码中仍然残留了其他 ES2015+ 的特性，我们希望对它们也进行转换。我们不需要一个接一个地添加所有需要的插件，我们可以使用一个 "preset" （即一组预先设定的插件）。

  preset   就是对一些常用的插件，批量配置。



### 那么有哪些插件呢

### ES3

- [成员表达文学](https://babel.docschina.org/docs/en/babel-plugin-transform-member-expression-literals)
- [财产文学](https://babel.docschina.org/docs/en/babel-plugin-transform-property-literals)
- [保留字](https://babel.docschina.org/docs/en/babel-plugin-transform-reserved-words)

### ES5

- [财产突变者](https://babel.docschina.org/docs/en/babel-plugin-transform-property-mutators)

### ES2015

- [箭头函数](https://babel.docschina.org/docs/en/babel-plugin-transform-arrow-functions)
- [块作用域函数](https://babel.docschina.org/docs/en/babel-plugin-transform-block-scoped-functions)
- [块作用域](https://babel.docschina.org/docs/en/babel-plugin-transform-block-scoping)
- [班级](https://babel.docschina.org/docs/en/babel-plugin-transform-classes)
- [计算属性](https://babel.docschina.org/docs/en/babel-plugin-transform-computed-properties)
- [解构](https://babel.docschina.org/docs/en/babel-plugin-transform-destructuring)
- [重复键](https://babel.docschina.org/docs/en/babel-plugin-transform-duplicate-keys)
- [换取](https://babel.docschina.org/docs/en/babel-plugin-transform-for-of)
- [功能名称](https://babel.docschina.org/docs/en/babel-plugin-transform-function-name)
- [实例](https://babel.docschina.org/docs/en/babel-plugin-transform-instanceof)
- [文字](https://babel.docschina.org/docs/en/babel-plugin-transform-literals)
- [新目标](https://babel.docschina.org/docs/en/babel-plugin-transform-new-target)
- [超级对象](https://babel.docschina.org/docs/en/babel-plugin-transform-object-super)
- [参数](https://babel.docschina.org/docs/en/babel-plugin-transform-parameters)
- [速记属性](https://babel.docschina.org/docs/en/babel-plugin-transform-shorthand-properties)
- [传播](https://babel.docschina.org/docs/en/babel-plugin-transform-spread)
- [粘性正则表达式](https://babel.docschina.org/docs/en/babel-plugin-transform-sticky-regex)
- [模板文字](https://babel.docschina.org/docs/en/babel-plugin-transform-template-literals)
- [符号类型](https://babel.docschina.org/docs/en/babel-plugin-transform-typeof-symbol)
- [unicode转义](https://babel.docschina.org/docs/en/babel-plugin-transform-unicode-escapes)
- [unicode-正则表达式](https://babel.docschina.org/docs/en/babel-plugin-transform-unicode-regex)

### ES2016

- [求幂运算符](https://babel.docschina.org/docs/en/babel-plugin-transform-exponentiation-operator)

### ES2017

- [异步发电机](https://babel.docschina.org/docs/en/babel-plugin-transform-async-to-generator)

### ES2018

- [异步发电机功能](https://babel.docschina.org/docs/en/babel-plugin-proposal-async-generator-functions)
- [正则表达式](https://babel.docschina.org/docs/en/babel-plugin-transform-dotall-regex)
- [命名捕获组正则表达式](https://babel.docschina.org/docs/en/babel-plugin-transform-named-capturing-groups-regex)
- [对象静止传播](https://babel.docschina.org/docs/en/babel-plugin-proposal-object-rest-spread)
- [可选捕获绑定](https://babel.docschina.org/docs/en/babel-plugin-proposal-optional-catch-binding)
- [unicode-property-regex](https://babel.docschina.org/docs/en/babel-plugin-proposal-unicode-property-regex)



### 那么 有哪些预设呢

我们为常见环境组装了一些 presets ：

- [@babel/preset-env](https://babel.docschina.org/docs/en/babel-preset-env)
- [@babel/preset-flow](https://babel.docschina.org/docs/en/babel-preset-flow)
- [@babel/preset-react](https://babel.docschina.org/docs/en/babel-preset-react)
- [@babel/preset-typescript](https://babel.docschina.org/docs/en/babel-preset-typescript)



安装预设   （preset）

案例：   以第一个为例

npm install --save-dev @babel/preset-env  

编译指令   （ 下面这种指令， 是在没有`.babelrc` 文件，情况下）

```
./node_modules/.bin/babel src --out-dir lib --presets=@babel/env  
```

简写： 

npx babel src --out-dir lib --presets=@babel/preset-env

( ，npm 从5.2版开始，增加了 npx 命令。   他会自动去node_modules，寻找babel的执行文件 )



！ 注意点：  

如果执行npx 没成功， 删掉依赖， npm i ,  再试

配置文件中， @babel/preset-env  刚才npm了什么插件，就用那个名字，版本经常变，需要注意。





查看编译后文件： 发现  let   => var   ()={}    箭头函数变了    ； import   变成了es6  的 require



再次改进： 

根目录中 添加

`.babelrc` 文件

```
{
  "presets": ["@babel/preset-env"]
}
```



指令简化： 

npx babel src --out-dir lib   

在配置了`.babelrc` 文件 后， 代码会自动去使用配置文件。告诉他使用那些插件去编译。 



## Polyfill

模块包含 [core-js](https://github.com/zloirock/core-js) 和一个自定义的 [regenerator runtime](https://github.com/facebook/regenerator/blob/master/packages/regenerator-runtime/runtime.js) 来模拟完整的 ES2015+ 环境。

这意味着你可以使用诸如 `Promise` 和 `WeakMap` 之类的新的内置组件



# 结合webpack 

使用webpack，先 下载插件

```bash
npm install webpack webpack-cli --save-dev
```



新建webpack.config.js

配置项，定义 入口文件，出口文件， 输出文件的名字，输出的路径。

```
const path = require('path');

module.exports = {
                mode:"development",
  entry: './lib/2.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
};
```

编译指令：

```
默认  npx webpack --config webpack.config.js
   可简写：npx webpack   如果不是这个js文件， 需要指定路径名字。
```

执行编译可能会提示的warning.     表示： 打包是生产模式，还是测试模式

WARNING in configuration
The 'mode' option has not been set, webpack will fallback to 'production' for this value. Set 'mode' option to 'development' or 'production' to enable defaults for each environment.



index.html文件 最终使用bundle.js就行了。

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="../dist/bundle.js"></script>
</head>

<body>
    <h1>babel测试</h1>
</body>
<script>
    var p = new Promise(function (resolve, reject) {
        setTimeout(() => {
            resolve()
        }, 1000);

    }).then(() => {
        alert("ok")
    })
</script>

</html>
```



结论：

babel 通过babel配置文件，规定通过什么插件，编译成什么文件， 然后webpack， 通过webpack.config.js配置文件，规定了编译那个文件（把babel编译后的js作为入口文件），编译后放到那个位置。



## 上接 polyfill 垫片

注意，使用 `--save` 参数而不是 `--save-dev`，因为这是一个需要在你的源码之前运行的 polyfill。

--save-dev 是开发依赖， webpack会把 package.json里的dev*dependencies* ，*dependencies* 都  进行打包。



从 Babel 7.4.0 开始，这个包已经被弃用，以支持直接包含`core-js/stable`（以 polyfill ECMAScript 功能）和`regenerator-runtime/runtime`（需要使用转译的生成器函数）



#### 在 Node / Browserify / Webpack 中的使用

要包含 polyfill，您需要在应用程序**入口点**的顶部要求它。

> 确保在所有其他代码/要求语句之前调用它！

```
import "@babel/polyfill";
确保，入口文件的顶端。

```

总结： 一个插件，解决一个问题。 预设： 包含一批插件。 目前有4个预设。 

插件： 有测试版， 预设版



# webpack

#### loader  

babel只能处理js文件。 css， font文件，需要其他插件。    webpack- loader 配置项，来处理。

webpack 只能理解 JavaScript 和 JSON 文件。**loader** 让 webpack 能够去处理其他类型的文件，并将它们转换为有效。例如： js文件中， 引入了字体文件， css文件，原则上是不能混装的， 但是，有了对应的loader, webpack，会进行分拣资源。 打包后的文件，类型分门别类。 方面了开发。

#### 那么，有哪些loader呢   ？

https://v4.webpack.docschina.org/loaders/

```

babel-loader           ----（bebel 作为webpack loader 模块中的一个组成部分）
yaml-frontmatter-loader
cache-loader
coffee-loader
coffee-redux-loader
config-loader
coverjs-loader
css-loader
.....
```

#### 使用loader

oader 通过在 `require()` 语句中使用 `loadername!` 前缀来激活，或者通过 webpack 配置中的正则表达式来自动应用 - 查看[配置](https://v4.webpack.docschina.org/concepts/loaders#configuration)。

```
rules: [
      { test: /\.css$/, use: 'css-loader' },
      { test: /\.ts$/, use: 'ts-loader' }
    ]
```



tips:  查看每种文档的时候，不要手忙脚乱，先从指南，使用指南入手。

webpack 指南。

https://v4.webpack.docschina.org/guides/installation/#%E9%A2%84%E5%85%88%E5%87%86%E5%A4%87

第一步： 安装

```shell
npm install --save-dev webpack
如果你使用 webpack v4+ 版本，你还需要安装 CLI



```

webpack -v    5.15.0   webpack  核心方法

webpack-cli 3.3.12    集成了部分 创建项目的快捷系列指令。 （脚手架，方便创建标准配置项目）

案例：

使用babel 环境，安装jquery

https://www.npmjs.com/package/   npm插件市场， 搜索jquery

1 查到 Browser 环境下使用方法：

```
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
```

2 查到 babel环境下使用方法

```
import $ from "jquery";
```

这里使用第2种

先下载，在引入

cnpm install jquery --save （需要明确一点， jquery生产依赖，不是开发依赖 --save）

```

import "@babel/polyfill";
import $ from "jquery";

import { test, test2} from "./1.js" ;

test();
test2();

$(function(){

    $("body").css({backgroundColor:"red"})
})()
```

打包命令： 

npx babel src --out-dir lib

webpack 

执行后，运行index.html  效果出现

#### 加载  .css文件后缀的文件

https://v4.webpack.docschina.org/guides/asset-management/#%E5%8A%A0%E8%BD%BD-css

## 加载 CSS 文件

为了在 JavaScript 模块中 `import` 一个 CSS 文件，你需要安装 [style-loader](https://v4.webpack.docschina.org/loaders/style-loader) 和 [css-loader](https://v4.webpack.docschina.org/loaders/css-loader)，并在 [`module` 配置](https://v4.webpack.docschina.org/configuration/module) 中添加这些 loader：

```
npm install --save-dev style-loader css-loader    这包含了两个api  一个style-loader 一个css-loader
```

**webpack.config.js**

```
 module: {
+     rules: [
+       {
+         test: /\.css$/,
+         use: [
+           'style-loader',
+           'css-loader'
+         ]
+       }
+     ]
+   }
```

入口js

```

import "@babel/polyfill";
import $ from "jquery";
import "./style.css" ;      

import { test, test2} from "./1.js" ;

test();
test2();

$(function(){
    $("body").css({backgroundColor:"red"})
})()
```

  注意点：

 源代码 --- babel编译代码 --- moudle.js

（ style.css放到中间，babel编译后的文件一起，原因是，webpack 编译的目标文件，就是babel处理过的文件）



## 图片loader 

```bash
npm install --save-dev file-loader
```

**webpack.config.js**

```
{
+         test: /\.(png|svg|jpg|gif)$/,
+         use: [
+           'file-loader'
+         ]
+       }
```

npx babel src --out-dir lib

npx webpack

打包后，发现：

dis文件夹下：

```
|- package.json
  |- webpack.config.js
  |- /dist
    |- bundle.js
    |- index.html
    |- fa5aacd030eddc85f28c03cf70417bbd.png
    发现图片并没有打包到bundle.js中，而是重新命名，原原本本的移动过去， 所以真实的项目中，并不适用，用到图片，可以直接放到静态资源中，不必打包。
    
```

## 加载数据 

此外，可以加载的有用资源还有数据，如 JSON 文件，CSV、TSV 和 XML。类似于 NodeJS，JSON 支持实际上是内置的，也就是说 `import Data from './data.json'` 默认将正常运行。要导入 CSV、TSV 和 XML，你可以使用 [csv-loader](https://github.com/theplatapi/csv-loader) 和 [xml-loader](https://github.com/gisikw/xml-loader)。让我们处理加载这三类文件：

案例： 加载json

入口js 中，引入，可以直接使用

```
import data from "./json/data.json";


console.log(data)
```



### babel-loader

背景：    源代码----   babel编译后的代码 -- --  webpack编译后的代码

前面，学习babel  webpack 操作过程，可以发现， 每次我们需要编译两次。  babel 编译， webpack编译， 显然不利于开发，那么如何操作一次，完成同样的效果。 babel-loader 的作用，就是这个。

第一步： 安装

babel 经常升级，并且经常出现兼容问题   npm插件市场上，搜索 babel-loader

https://www.npmjs.com/package/babel-loader

注意点：

此自述文件适用于 babel-loader v8 + Babel v7 如果您使用的是旧版 Babel v6，请参阅[7.x 分支](https://github.com/babel/babel-loader/tree/7.x)文档



```
npm install -D babel-loader @babel/core @babel/preset-env webpack
```



检查; package.json ,  babel-loader v8 + Babel v7 , 版本是否对应，否则不兼容。

第二步：

检查项目目录结构

```
webpack-demo
     .babelrc
  |- dis
  |- package.json
  |- index.html
  |- /src
    |- img
    |- css
    |- js
    
    删除了lib, 因为已经不需要，代码中转， 只用插件直接打包生成dis文件夹
```

第三步：

配置 webpack.config.js

在 webpack 配置对象中，需要将 babel-loader 添加到 module 列表中，就像下面这样：

```
module: {
  rules: [
    {
      test: /\.m?js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
    //    options: {
      //    presets: ['@babel/preset-env']
      //  }
      }
    }
  ]
}
配置： 告诉了webpack， 匹配什么后缀的文件， 哪些文件夹不需要编译， 使用什么loader,chajian yong nayige .

```

注意点：  此时关于babel 的配置，这里可能重复。presets: ['@babel/preset-env']， 插件指定， 因为有一个.babelrc 专门的babel配置文件，  webpack.config.js里也可以配置这一块， 所以可能重复。处理办法是：

  //    options: {
      //    presets: ['@babel/preset-env']
      //  }   这里一项， 删掉。关于babel的配置， 都写在bebel的配置文件中 。 



调整打包路径

```
 entry: './src/2.js',
```

  npx  webpack         打包成功  （一个命令实现）

下面是配置文件

webpack.config.js

```
const path = require('path');

module.exports = {
  mode: "development",
  entry: './src/2.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader'
        ]
      },
      {
        test: /\.(png|svg|jpg|gif)$/,
        use: [
          'file-loader'
        ]
      },
      {
        test: /\.m?js$/,
        exclude: /(node_modules|bower_components)/,
        use: {
          loader: 'babel-loader'
        }
      }
    ]
  }
};

```

### 自定义指令 + 热加载

我们发现，每次打包需要输入 

npx webpack     ,  而执行某个特定js, 需要输入较长的路径。 有没有快捷方法，有的。

[使用 watch mode(观察模式)](https://v4.webpack.docschina.org/guides/development/#%E9%80%89%E6%8B%A9%E4%B8%80%E4%B8%AA%E5%BC%80%E5%8F%91%E5%B7%A5%E5%85%B7)

**package.json**  

```
  {
    "name": "development",
    "version": "1.0.0",
    "description": "",
    "main": "webpack.config.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
+     "watch": "webpack --watch",
      "build": "webpack"
    },
    

```

使用： npm run  build   编译一次

npm run  watch  监控代码改变，改变自动编译。 刷新浏览器，可以看到改变。



### 再次改进

能不能，修改代码后，浏览器自动刷新浏览器，               使用 webpack-dev-server 插件

​         `webpack-dev-server` 为你提供了一个简单的 web server，并且具有 live reloading(实时重新加载) 功能。设置如下：     

```bash
npm install --save-dev webpack-dev-server
```

 *"webpack-dev-server"*: "^3.11.2"

修改配置文件，告诉 dev server，从什么位置查找文件：

**webpack.config.js**

```
  const path = require('path');
  const HtmlWebpackPlugin = require('html-webpack-plugin');
  const CleanWebpackPlugin = require('clean-webpack-plugin');

  module.exports = {
    mode: 'development',
    entry: {
      app: './src/index.js',
      print: './src/print.js'
    },
    devtool: 'inline-source-map',
+   devServer: {
+     contentBase: './dist'
+   },
    plugins: [
      new CleanWebpackPlugin(['dist']),
      new HtmlWebpackPlugin({
        title: 'Development'
      })
    ],
    output: {
      filename: '[name].bundle.js',
      path: path.resolve(__dirname, 'dist')
    }
  };
```





配置完后，无法自动跑起来

#### [webpack编译遇到的问题：Error: Cannot find module 'webpack-cli/bin/config-yargs'](https://www.cnblogs.com/jeacy/p/13864454.html)

**运行`npm run dev`遇到的问题：Error: Cannot find module 'webpack-cli/bin/config-yargs'**



**解决：**

1. 卸载当前的 webpack-cli `npm uninstall webpack-cli`
2. 安装 webpack-cli 3.* 版本 `npm install webpack-cli@3 -D`



成功运行......

总结：  在整个过程中， 安装依赖，经常出现未找到依赖， 处理方式，删掉，重新install。 

 查看插件的版本， 如 vue cli的版本问题。



tips：

```
npm install rimraf -g 

// 使用命令删除 
rimraf node_modules // 也可以删除其它文件夹或文件
```

实战演练：

vue项目中， 使用可选链



npm install --save --dev @babel/plugin-proposal-optional-chaining





cnpm uninstall --save-dev babel-polyfill

