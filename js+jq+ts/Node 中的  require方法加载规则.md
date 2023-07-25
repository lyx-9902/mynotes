##  Node 中的  require方法加载规则

### 一   exports 方法加载模块分为三种

###    1.核心模块

```
require('模块标示')
1.如果是非路径形式的模块标识  即加载核心模块
require('fs')   //为什么可以这样写   官方把方法写入到了node.js程序中了。
https://github.com/nodejs/node/blob/master/lib/fs.js  //可以参照源码
核心模块的本质也是文件, 文件已经被编译到二进制文件中,我们只需要按照名字来加载就可以了
```



### 2..路径形式的模块

```
2.路径形式的模块
require('./foo.js')  //js可以省略
   ./ 当前目录,不可省略
   ../上一级目录,不可省略
   /xxx        几乎永不
  绝对路径  d:a/foo.js   几乎不用,
   首位的 / 在这里表示的是当前文件模块所属磁盘跟路径
   
```



### 3.第三方的包 模块

```
 require('art-template')

凡是第三方的模块,都需要通过npm 来下载
   使用的时候通过require('包名') 的方式来进行加载 才可以使用.
   不可能有任何一个第三方包和核心模块的名字是一样的.  [因为引入方式都是一样,不就混淆了]
   就是说,npm在发布的时候,就会审核,不允许有名字重复的包名字.
   
   加载逻辑:
    1.先判断是否为核心模块  No
    2. 判断是否为路径形式 No
    3. 举例子: art-template的安装.,
         首先在 在当前路径下找到node_modules目录, 如果有,进行下一步
        node_modules/art-template[ 这个名字就是npm i 装包的时候的名字]
        如果有,查看node_modules/art-template/packgge.json文件
        找文件中的main属性 ,属性指向一个js文件,默认是index.js
        main属性中记录了art-template的入口模块,然后加载使用这个第三包/
        一般是 这样  "main": "index.js",
        如果package.json文件不存在或者main指定的入口模块是错的,
        那么node会自动找该目录下的index.js
        
        如果以上所有任何一个条件都不成立,则会进入上一级目录中查找node_modules中,
        如果上一级还没有,再上一级,直到根目录.
        
```



# 测试：

![1593624132242](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1593624132242.png)



b.js  中写入

```
require('aa')
```

 1.先判断是否为核心模块  No  

 2. 判断是否为路径形式 No     

3.当前路径下找到node_modules目录
node_modules/  aa  /package.json

   packgge.json 中查找     {    "main": "index.js",  }  定位到当前目录的index.js。  最终执行这个文件。