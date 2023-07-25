# webpack 笔记精讲

## 小知识点：

webpck官方地址 : https://webpack.docschina.org/guides/getting-started/#basic-setup

#### nrm 

nrm(npm registry manager )是npm的镜像源管理工具，有时候国外资源太慢，使用这个就可以快速地在 npm 源间切换

nrm ls  展示所有镜像列表

```
带星号的是 当前正在使用的镜像。 
npm -------- https://registry.npmjs.org/
  yarn ------- https://registry.yarnpkg.com/
  cnpm ------- http://r.cnpmjs.org/
* taobao ----- https://registry.npm.taobao.org/
  nj --------- https://registry.nodejitsu.com/
  npmMirror -- https://skimdb.npmjs.com/registry/
  edunpm ----- http://registry.enpmjs.org/
作用就是： 当你npm install 的时候，会从星号的地址上下载资料包。
```

cls清屏

 1   基本安装

```
mkdir webpack-demo
cd webpack-demo
npm init -y     初始化工程 生成packge.json 文件(当你第一次npm下载包后，出现 package-lock.json，记录包的下载地址信息)
```

关于命令行指令的简写

Node 8.2/npm 5.2.0 以上版本提供的 `npx` 命令，可以运行在初次安装的 webpack package 中的 webpack 二进制文件（即 `./node_modules/.bin/webpack`）

## 1 webpack 执行指令

```
.\node_modules\.bing\webpack -v
```

等同于 npx webpack -v

案例测试：

```
  webpack-demo
  |- package.json
  |- webpack.config.js
  |- src
    |- main.js
    |- dis
    
执行    npx webpack .\src\main.js -o \src\dist\boundle.js 
         打包main.js， 输出到当前目录中的dist文件夹，生成 bundle.js
```

## 打包指令改进

加入配置文件概念 **webpack.config.js**

#### 配置入口和出口

```
const path = require('path');

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
};
```

接下来指令 就不需要再加 输入和输出的内容了 。 指令如下

npx webpack

## 2 使用插件热加载

### webpack-dev-server  热加载

```bash
npm install --save-dev webpack-dev-server
```

**webpack.config.js**

```diff
  devServer: {
+    contentBase: './dist',
+  },
```

**package.json**

```
   "start": "webpack serve --open",
```

现在，在命令行中运行 `npm start`

```
开发辅助插件
"devDependencies": {
    "webpack-dev-server": "^3.11.2"
  }  
```

注意点： 打包后的文件，没有放到磁盘上，而是放到了内存上。 http://localhost:8080/boundle.js 可以查看到

调整： index.html

   <script src="/boundle.js"></script>  直接引用内存上的编译文件。  好处： 提高访问速度

修改打开端口

```
"start": "webpack serve --open --port 3000"
```

注意点： 一个端口，只能打开一个服务，不能重复。

##### 打包优化： 

 项目代码，修改了那些代码，就打包那些代码

**package.json**

```
  "start": "webpack serve --open --port 3000 --hot"        关键指令 --hot
```

或者在**webpack.config.js**

```
   devServer: {
        contentBase: 'src/',
        open:true,
        port:3000,
        hot:true
      },
```

两种方式都可以。但一般采用第二种。

## 3 loader

作用：loader 用于对模块的源代码进行转换。   除js外其他webpack不认识的资源，进行处理

#### 案例1：css -loader 

  解决的问题：   main.js中  引入css文件

**main.js**

```
import $ from "jquery"
$(function(){
    $("li:odd").css("backgroundColor","#fff")
    $("li:even").css("backgroundColor","#B9F444")
})

import "./css/style.css"
```

所有的loader遵循 先安装，再配置，再使用。 

```bash
npm install --save-dev css-loader
```

**webpack.config.js**

```
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [ 'style-loader', 'css-loader' ]
      }
    ]
  }
}
```

查看官网配置案例，发现css-loader还依赖style-loader。 所以查找配置项，同样安装一下。

```
 npm install style-loader --save-dev
```

启动项目，发现已经不报错了。

### 案例2：less -loader  

解决的问题： main.js中引入less样式文件。让webpack可以正常解析。

在本地css文件中，创建一个less文件，然后引入main.js中。

安装：  

```bash
npm install --save-dev less-loader less
```

上面指令，安装了两个， 一个是less， 一个是less-loader

```js
// webpack.config.js
module.exports = {
    ...
    module: {
        rules: [{
            test: /\.less$/,
            use: [{
                loader: "style-loader" // creates style nodes from JS strings
            }, {
                loader: "css-loader" // translates CSS into CommonJS
            }, {
                loader: "less-loader" // compiles Less to CSS
            }]
        }]
    }
};
```

上面我们可以看到，针对less结尾的文件，他使用了三种loader。

配置好后，运行

### 其他如： 图片和sass-loader 用法相同



## 4 插件的使用

作用： loader处理不了的需求，由插件进行处理

案例：HtmlWebpackPlugin     该插件将为你生成一个 HTML5 文件

安装

```
npm install --save-dev html-webpack-plugin
```

配置

```
var HtmlWebpackPlugin = require('html-webpack-plugin');
var path = require('path');

var webpackConfig = {
  entry: 'index.js',
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: 'index_bundle.js'
  },
    plugins: [new HtmlWebpackPlugin(
        {
            template: 'src/index.html',  
            filename: 'index.html',
        }
    )],
};
```

这将会产生一个包含以下内容的文件 `dist/index.html`：

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>webpack App</title>
  </head>
  <body>
    <script src="index_bundle.js"></script>
  </body>
</html>
```

解析： 

打开chrome 调试页面可以查看到，dom如上面所示。 本地本目录中没有index_bundle.js， html-webpack-plugin创建的index.html也没发现。原因是：

webpack-dev-server  根据配置项要求， 把打包后的index_bundle.js，html-webpack-plugin创建的index.html， 放到了内存中。 浏览器中可以查看，但是本地目录中没有。 

## 5  webpack 集成bootstrap的使用

查看bootstrap官网，得知 其依赖jquery.

**安装jQuery**

```
npm install jquery --save-dev
```

**安装bootstrap**

```
npm install bootstrap --save-dev
```

引入一个概念：  main.js中加载这js ，css. less  TTF字体图标 等， loader们都可以通过正则匹配，逐个解析掉。但是是，bootstrap   jQuery 都是单独的插件， 插件和插件之间有依赖关系，这个不能解决。

所以引入  webpack.ProvidePlugin

查看官网作用是： 自动加载模块，而不必到处 `import` 或 `require` 

要自动加载 `jquery`，我们可以将两个变量都指向对应的 node 模块：

```javascript
new webpack.ProvidePlugin({
  $: 'jquery',
  jQuery: 'jquery'
}
```

解决方案：
在 webpack.base.conf.js 头部添加

```
var webpack = require('webpack')
```


在 entry 后边添加

```
  plugins: [
      new webpack.ProvidePlugin({
          "$": "jquery",
          "jQuery": "jquery",
          "window.jQuery": "jquery"
      })
  ]
```

注意点： 本案例使用   *"bootstrap"*: "^3.4.1", 

  bootstrap中使用了字体图标， loader一定要设置。

```
  {
                test: /\.(ttf|eot|svg|woff|woff2)$/,
                use: "url-loader",
            },
```



# 附加题

## babel.loader



![image-20210614192119347](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\image-20210614192119347.png)









