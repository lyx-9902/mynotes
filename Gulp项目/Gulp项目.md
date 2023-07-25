# Gulp项目

# gulp搭建前端项目

gulp官方API

 https://www.gulpjs.com.cn/docs/api/concepts/

# 前言

前端技术发展日新月异，随着模块化、组件化的提出，前端变得越来越复杂，静态资源越来越多，那么对静态资源的处理，如压缩，合并，去掉调试信息.. 如果还是人工去处理，效率非常之低且还容易出错，于是自动化的处理工具也就必然出现了。就像后端我们一般用maven管理项目，那么前端gulp是个不错的选择。

# 什么是gulp

是一个基于 Node.js 流、Javascript语法的快速构建前端项目并减少频繁的 IO 操作的自动化工具。

```
cnpm install gulp  --save-dev
```

npm install gulp  --save-dev



##  第一部分：Gulp项目初次创建可能碰到的问题

### 1 概念：

gulp是一个自动化构建工具，主要用来设定程序自动处理静态资源的工作。简单的说，gulp就是用来打包项目的。  技术基础：依赖node的一个工具；所以node的版本和gulp的版本有变化，项目会出现各种报错。新手经常踩的坑。

### 2 工作原理和逻辑：

gulp是一个基于任务的工具，也就是说，gulp规定，不管做什么功能，都用统一的接口管理，必须去注册一个任务，然后去执行这个任务，在任务代码中，去做想想做的功能。

###### 特点之一基于流。

gulp自己有内存，当我们使用gulp进行项目构建的时候，gulp会将本地文件数据读取到gulp内存中，接下来的操作都在内存中进行，操作完成以后，再从gulp的内存中输出到本地，比如说当我们要合并两个文件的时候，先将这两个文件中的内容读取到内存中，然后在内存中进行合并，最后将合并后的内容从内存中输出到本地的文件中。

这样，对应着两个操作，一个是输入，一个输出，也就是I/O操作。这是gulp的又一个特点之一：基于流。

###### 特点之二：任务化。

gulp的每个功能都是一个任务，压缩css的任务、合并文件的任务。。。gulp规定任务要写在一个叫做glupfile.js的文件中，在这个文件中用来配置所有任务。

首先，gulp和node中的其他模块一样，使用的时候需要引入：

```
varglup=require("gulp");
```

这个gulp是一个对象，gulp提供了很多接口，都是这个对象的方法。

### 3 几个主要的APIgulp插件

```
 src 
 注册任务 task  
```

#### 3.1  less 

```
npm install gulp-concat gulp-uglify gulp-rename --save-dev

 less 和css压缩
 npm install gulp-less gulp-clean-css --save-dev

```

#### 3.2 html的压缩插件

```
npm install gulp-htmlmin --save-dev
var htmlmin = require("gulp-htmlmin")
```

#### 3.3 自动编译插件

作用是：修改less文件后，自动编译less成css。 但是需要手动刷新页面； （有称半自动辅助插件）

```
npm install gulp-livereload --save-dev
var livereload = require("gulp-livereload")

// 创建代码监听 - 热加载
gulp.task('watch', ['default'], function () {
    // 开启监听
    liverReload.listen();
    // 确认监听的目标和绑定响应的任务
    gulp.watch('src/js/*.js', ['js']);
    gulp.watch(['src/css/*.css', 'src/less/*.less'], ['css']);

})
然后在其他任务加刷新管道指令
```

#### 3.4  热加载（实时加载）

​      功能： 该插件内置一个服务api。可以启动一个服务。实时更新页面。（与自动编译插件合称 项目全自动组件）

```
1 npm install gulp-connect --save-dev
2 注册热加载的任务 server ，注意依赖build任务。
3 注册热加载的选项
配置加载的选项
  connect = require('gulp-connect'),
```

  1  首先穿件server服务；2  在其他任务中都加入管道   ` .pipe(connect.reload())` 3. 监听那些文件变化

完整案例如下：

```
gulpfils.js文件

const gulp = require('gulp'),
    concat = require("gulp-concat"),
    rename = require('gulp-rename'),
    less = require('gulp-less'),
    cleanCSS = require('gulp-clean-css'),
    htmlMin = require('gulp-htmlmin'),
    liverReload = require('gulp-livereload'),
    connect = require('gulp-connect'),
    uglify = require("gulp-uglify");


// 创建文件合并任务
gulp.task("js", () => {
    return gulp.src("./src/js/*.js") //要合并的 js 文件
        .pipe(concat('all.js')) //创建临时合并文件
        .pipe(gulp.dest("dist/js")) // 
        .pipe(uglify()) // 压缩文件
        .pipe(rename({
            suffix: ".min"
        })) // 重命名
        .pipe(gulp.dest('dist/js/'))
        .pipe(liverReload()) // 自动更新
        .pipe(connect.reload())
})
// 创建任务- less 编译和压缩
gulp.task("less", () => {
    return gulp.src("./src/less/*.less")
        .pipe(concat('all.css')) //创建临时合并文件
        .pipe(less()) // 压缩文件
        .pipe(gulp.dest("./src/css/"))
        .pipe(liverReload()) // 自动更新
        .pipe(connect.reload())
})
// 创建任务- css合并压缩
gulp.task("css", () => {
    return gulp.src("./src/css/*.css")
        .pipe(concat('all.css')) //创建临时合并文件
        .pipe(gulp.dest("dist/css/"))
        .pipe(liverReload()) // 自动更新
        .pipe(connect.reload())
})
// 创建任务- html合并压缩
gulp.task("html", () => {
    return gulp.src("./src/index.html")
        .pipe(htmlMin({
            collapseWhitespace: true
        }))
        .pipe(gulp.dest('dist/'))
        .pipe(liverReload()) // 自动更新
        .pipe(connect.reload())
})


// 创建代码监听 - 热加载
gulp.task('watch', ['default'], function () {
    // 开启监听
    liverReload.listen();
    // 确认监听的目标和绑定响应的任务
    gulp.watch('src/js/*.js', ['js']);
    gulp.watch(['src/css/*.css', 'src/less/*.less'], ['less','css']);
    gulp.watch('src/index.html', ['html']);

})

//  创建服务
gulp.task('server', ['default'], function () {
    connect.server({
        root: "dist/", // 指定根目录
        livereload: true, // 实时刷新
        port: 5000  //定义端口  （ip 不指定是 默认localhost）
    })
    // 确认监听的目标和绑定响应的任务
    gulp.watch('src/js/*.js', ['js']);
    gulp.watch(['src/css/*.css', 'src/less/*.less'], ['less','css']);
    gulp.watch('src/index.html', ['html']);
})


gulp.task('default', ['js', 'less', 'css', 'html'])
```

#### 3.5 自动打开浏览器 open

```
npm install open --save-dev

配置：方法到serve中间
//  创建服务
gulp.task('server', ['default'], function () {
    connect.server({
        root: "dist/", // 指定根目录
        livereload: true, // 实时刷新
        port: 5000  //定义端口  （ip 不指定是 默认localhost）
    })
    // 自动打开指定链接
    open("http://localhost:5000/")

    // 确认监听的目标和绑定响应的任务
    gulp.watch('src/js/*.js', ['js']);
    gulp.watch(['src/css/*.css', 'src/less/*.less'], ['less', 'css']);
    gulp.watch('src/index.html', ['html']);
})
```



#### 3.6 插件集合 

 功能是：按需引入改为 简单的全部引入

```
npm install gulp-load-plugins

var $ = require('gulp-load-plugins')
注意点：
  合集中包含的api 为报名为gulp- 开头的对象。
  
这些不包含
var gulp = require('gulp');
var open = require('open');
这些包含
var concat = require("gulp-concat");
var uglify = require("gulp-uglify");
var rename = require('gulp-rename');
var less = require('gulp-less');
var cssClean = require('gulp-clean-css');
var htmlMin = require('gulp-htmlmin');
var liverReload = require('gulp-livereload');
var connect = require('gulp-connect');
在替换时： 需要注意两种情况
gulp-concat  使用$.concat 默认包名
gulp-clean-css 使用$.cleanCss   
htmlmin          使用$.htmlmin   
```



4 任务的异步和同步

```
// 创建任务- css合并压缩
gulp.task("css", () => {
    return gulp.src("./src/css/*.css")
        .pipe(concat('all.css')) //创建临时合并文件
        .pipe(gulp.dest("dist/css/"))
})

当 gulp执行命令时， 编译异步； 当去掉return 时， 编译是同步。 默认异步
当任务之间有依赖关系时，需要加参数。
gulp.task("css",['less'] () => { ... 表示css编译，依赖less执行完毕后

```



[其他插件参考：](https://blog.csdn.net/qq_38334525/article/details/103123031?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.no_search_link&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.no_search_link)

### 安装：

全局安装：

npm i gulp@3.9.1 -g

gulp -v # 测试是否安装成功

全局安装表示在当前电脑中可以使用gulp环境了

局部安装

npm i gulp@3.9.1 --save-dev # 因为在上线后是不需要这个包的，所以将这个项目安装在开发依赖

局部安装表示在当前项目要使用的gulp

局部安装gulp要和全局安装的gulp版本保持一致





官网：[https://gulpjs.com/](https://links.jianshu.com/go?to=http%3A%2F%2Flink.zhihu.com%2F%3Ftarget%3Dhttps%3A%2F%2Fgulpjs.com%2F)

中文官网：[https://www.gulpjs.com.cn/docs/](https://links.jianshu.com/go?to=http%3A%2F%2Flink.zhihu.com%2F%3Ftarget%3Dhttps%3A%2F%2Fwww.gulpjs.com.cn%2Fdocs%2F)

#### 当我们在使用gulp的时候，gulp到底用来干什么呢？

1. 编译 sass
2. 合并优化压缩 css
3. 校验压缩 js
4. 优化图片
5. 添加文件指纹（md5）
6. 组件化头部底部（include html）
7. 实时自动刷新…
8. ......
9. 压缩静态资源
10. 变更静态资源
11. 给静态资源添加 md5
12. 修改预处理样式后自动编译（SASS，Less）
13. 合并雪碧图
14. 自动刷新浏览器
15. ......
16. Sass编译
17. Css Js 图片压缩
18. Css Js 合并
19. Css Js 内联
20. Html的include功能
21. Autoprefixer
22. 自动刷新
23. 去缓存
24. Handlebars模板文件的预编译
25. 雪碧图
26. ESLint
27. rem移动端适配方案

## 第二部分：创建 Gulp demo

```cpp
npm config set registry http://registry.cnpmjs.org/
```

### 进入项目文件，安装本地gulp环境

```undefined
全局安装   npm install gulp -g
局部安装   npm install gulp --save-dev
```

### 新建gulpfile.js配置文件

用于创建项目任务

### 安装依赖包

```undefined
npm install
```

### 运行项目

```cpp
执行gulp，运行项目即可。
```





