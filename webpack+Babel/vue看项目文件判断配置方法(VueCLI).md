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

#### 安装  脚手架 Vue

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

## 1.2 环境配置的区别

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









