## 修改完代码自动重启

我们这里可以使用一个第三方命令行工具： `nodemon`  来帮我们解决频繁修改代码而重启服务器的问题。

nodemon是一个基于Nde.js开发的一个第三方命令行工具，我们使用的时候需要独立安装。

​      node  monitoring    node监视器

```
 cnpm install --global  nodemon  //全局安装  全局安装的包，在哪个目录中都可以装
 
版本检查： 
  nodemon --version
```

安装完毕后使用方法

```
node app.js

#  使用nodemon
cmd 命令行中输入： nodemon app.js     //nodemon js文件名字


接下来：在每次代码 strl+s时候， 就会自动执行

```

只要通过 nodemon app.js启动的服务，则他会监视你的文件变化，当文件变化的时候，自动帮你重启服务器。