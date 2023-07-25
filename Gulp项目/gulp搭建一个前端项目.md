# gulp搭建前端项目

gulp官方API

 https://www.gulpjs.com.cn/docs/api/concepts/

# 前言

前端技术发展日新月异，随着模块化、组件化的提出，前端变得越来越复杂，静态资源越来越多，那么对静态资源的处理，如压缩，合并，去掉调试信息.. 如果还是人工去处理，效率非常之低且还容易出错，于是自动化的处理工具也就必然出现了。就像后端我们一般用maven管理项目，那么前端gulp是个不错的选择。



## 1、安装nodejs

nodejs下载地址：https://nodejs.org/

nodejs自带npm模块管理器，安装完成之后打开dos命令窗口输入 node -v就能查看nodejs是否安装成成功

常用的npm命令

npm init——初始化

npm install——安装插件

npm install plugname -g——全局安装

npm install plugname@2.3.0——安装具体某个版本的插件

npm update——更新插件

npm uninstall——卸载插件

 

**常用dos命令**

cd 进入某个目录

cd.. 返回上一级

dir 查看列表

cls 清除屏幕

del name 删除文件

md name 新建目录名

rd name 删除目录名

copy con name.txt 新建文件

del name.txt 删除文件

## 2、全局安装gulp

```
npm install gulp -g
```

　　

## 3、创建本地项目

上面是准备工作，安装完全局gulp之后，cd到项目文件夹安装本地gulp，安装之前要先初始化

```
npm init
```

　初始化的时候要求你输入一些值，不输的直接回车即可，点击y之后在根目录自动创建了一个package.json文件，这个文件用来存放即将安装的插件name和version，这个文件有什么用呢？当我们把项目拷贝给别人的时候不需要拷贝插件，只需要把项目文件、package.json和gulp.file.js拷贝过去就可以，接收人cd到项目文件目录直接输入npm install即可安装上我们拷贝前安装的各种插件

## 4、设计项目目录索引结构

 

```undefined
└── src/
    ├── less/    *.less 文件
    ├── sass/    *.scss *.sass 文件
    ├── css/     *.css  文件
    ├── js/      *.js 文件
    ├── fonts/   字体文件
    └── images/   图片
└── dist/
```



## 5、安装各种插件

 

```
npm install gulp gulp-imagemin gulp-minify-css gulp-uglify gulp-util gulp-watch-path stream-combiner2 --save-dev
```

 

　　--save-dev这个命令是将安装的插件信息写入package.json文件内的“devDependencies”属性内，插件全部安装完之后package.json的变化为：

```
"devDependencies": {
    "gulp": "^3.9.1",
    "gulp-imagemin": "^2.3.0",
    "gulp-minify-css": "^1.2.4",
    "gulp-uglify": "^1.5.3",
    "gulp-util": "^3.0.7",
    "gulp-watch-path": "^0.1.0",
    "stream-combiner2": "^1.1.1"
  }
```



gulp——本地gulp
gulp-imagemin——图片压缩
gulp-minify-css ——css压缩
gulp-uglify ——js压缩
gulp-util ——控制台代码着色
gulp-watch-path ——文件很多时编辑那个哪个压缩，不会全部压缩（获取改变的文件的src和dest路径）
stream-combiner2——有些 gulp 任务编译出错会终止 `gulp.watch`，使用 `gulp-watch-path` 配合`stream-combiner2` 可避免这种情况

## 6、gulp如何使用

控制台输入gulp的时候首先找寻gulpfile.js文件，在找寻default任务，所以我们应该手动新建一个名为gulpfile.js的js文件，将任务写在里面。具体文件目录为：

![img](https://img-blog.csdn.net/20160601165619947?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

gulp一共五中方法：

gulp.task()——新建任务

gulp.src()——获取文件源地址

gulp.dest()——文件输出地址

gulp.run()——运行任务

gulp.watch()——监听文件修改

## 7、编写gulpfile.js文件



