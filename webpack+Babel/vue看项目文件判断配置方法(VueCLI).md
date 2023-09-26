# vue看项目文件判断配置方法

背景：你是否有过，配置项目的代理，开发环境，或者打包设置，重新启动项目，而没有生效？那么，你可能忽略了项目创建方式，和默认配置的作用。

# 1. Vue创建项目的几种方式

## 1.1. VueCLI提供的模板

在使用之前，可以先用 vue-list命令查询可用的模板

详解：

vue-cli提供了的常用的脚手架模板：

webpack：基于 webpack 和 vue-loader 的目录结构，而且支持热部署、代码检查、测试及 css 抽取。

webpack-simple：基于 webpack 和 vue-loader 的目录结构。

browerify：基于 Browerfiy 和 vueify(作用于 vue-loader 类似)的结构，支持热部署、代码检查及单元测试。

browerify-simple：基于 Browerfiy 和 vueify 的结构。

simple：单个引入 Vue.js 的 index.html 页面。

这里我们主要会使用 webpack 作为常用脚手架，可以运行vue init webpack my-project 来生成项目。





```
 版本目前有
vue CLI2  vue init webpack my-project   无可视化创建
vue CLI3  vue create my-project         vue ui可视化创建
vue CLI4  vue create my-project         vue ui可视化创建
vue CLI5  vue create my-project         vue ui可视化创建
```

明显区别是从vue CLI2后，vue-cli3.0 项目初始化方式，目前模版是固定的。模版选项可以自由配置，创建出来的是vue-cli3.0的项目，与vue-cli2.0项目结构不同，配置不同，具体配置方法参考官网。

vue init 是vue-cli2.0的项目初始方式，[webpack](https://so.csdn.net/so/search?q=webpack&spm=1001.2101.3001.7020)是官方推荐标准搭建

#### vue-cli的版本查看

```
vue -V
```

（测试自己的本地版本：2.9.6）



#### 不同脚手架版本下的命令和文件结构对比

### vue CLI2 

 ```
创建项目模板指令： vue init webpack project2
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

### 其他                     

```
创建项目模板指令： vue create my-project
模板结构：
--bublic
    |---favicon.ico
    |---index.html
--src
...
```

## 1.2 不同环境配置下的注意事项

### vue CLI2 

根目录下自动生成的有

```
--build
    |---webpack.base.conf.js
    |---build.js等等
--config   
    |---dev.env.js
    |---prod.env.js
--src
...
```

通过config文件下的js配置环境，build文件夹下js，配置webpack 其他的基础项。

注意点：本地测试发现 在VUE CLI2目录框架下，配置vue.config.js基本是无效的，说明build config文件下的配置优先级最高，比如配置项目前端服务跨域，要去   webpack.dev.conf.js文件

```

devServer: {

 headers: {
      "Access-Control-Allow-Origin": "*",
      "Access-Control-Allow-Headers": "*",
      "Access-Control-Allow-Methods": "*",
    },
}

```

这样才会有效果。

### 其他  

根目录下配置

vue.config.js文件 + 

.env.development, 

.env.production,

 .env.staging    

三个文件，来配置环境和环境变量，配置插件，启动命令，端口，打包等。

[参考文章](https://blog.csdn.net/baidu_30891377/article/details/106668574)

## 3.安装卸载和查看历史版本vue-cli

```
1.安装node.js（官网选择稳定版本或者推荐版本下载进行安装，傻瓜式安装即可，可以更改安装路径）
2.安装Vue-cli
（1）可能npm没有配置国内镜像,国外的仓库总是不容易拉取的，所以先换一下国内的镜像。

命令行输入"npm -g cnpm --registy=https://registry.npm.taobao.org"回车使用淘宝镜像

（2）然后进行Vue脚手架安装：
全局安装：命令行输入npm install vue-cli -g
指定版本的安装：命令行输入"npm install -g vue-cli@2.8.2"回车安装
npm安装指定版本的package，只需要在命令行之后加上 @版本号即可。

安装vue-cli 2.x指定版本
npm install -g vue-cli@2.x.x
//注意此处只有一个@

查看vue-cli3.x及以上可以安装的版本
npm view @vue/cli versions --json
安装：
例如 3.11.0版本
npm install -g @vue/cli@3.11.0

查看vue-cli2.x及以下可以安装的版本
npm view vue-cli versions --json

3.安装webpack
在 webpack3 中，webpack与webpack-cli是绑定的。也就是你使用"npm i webpack -g"安装了webpack以后，webpack-cli是默认就安装上了。但是到了webpack4，这2个东西已经被分解成了2个完全独立的包，所以，你还需要独立安装webpack-cli。

命令行输入 npm install webspack -g安装webpack。
命令行输入 npm i webpack-cli -g 安装webpack-cli。
输入webpack -v，查看安装成功。
```



————————————————
原文链接：https://blog.csdn.net/qq_43780814/article/details/112935636



## 4 升级VueGLi 可能碰到的问题

```

Vue packages version mismatch:

- vue@3.2.45 (C:\Users\15612\AppData\Roaming\npm\node_modules\vue\index.js)
- vue-template-compiler@2.7.14 (C:\Users\15612\AppData\Roaming\npm\node_modules\@vue\cli\node_modules\vue-template-compiler\package.json)

This may cause things to work incorrectly. Make sure to use the same version for both.
If you are using vue-loader@>=10.0, simply update vue-template-compiler.
If you are using vue-loader@<10.0 or vueify, re-installing vue-loader/vueify should bump vue-template-compiler to the latest.
```

提示： vue@3.2.45   vue-template-compiler@2.7.14 两个版本不对应。

npm i vue-template-compiler@3.2.45 --save

npm update vue-template-compiler



vueGLI版本和本地的vue模板版本不一致。需要匹配才可以。