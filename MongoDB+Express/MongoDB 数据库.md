



# 在 Exptess 中使用art-template 模板引擎

## 1. Install

```
npm install --save art-template
npm install --save express-art-template     两个都加载， 有相互依赖关系。
```

### 2. 配置使用 art-template 模板引擎

### 2.1 

第一个参数表示，当渲染以.art结尾的文件的时候，使用art-template模板引擎
express-art-template 是专门用来在Express 中 把art-template 整合到Express 中
虽然外面这里不需要加载art-template ,但是也必须要安装.
因为 express-art-template 依赖了art-template .

```
app.engine('art', require(express-art-template))
```

### 2.2

Express 为Response 相应对象提供了一个方法: render,
render 方法默认是不可以使用,但是如果配置了模板引擎就可以使用.
res.render('html模板名'， { 模板数据})
第一个参数不能写路径, 默认会去项目中的views 目录查找该模板文件.
也就是说Express 有一个约定: 开发人员把所有的视图文件都放到views目录中

 res.send("404.art")

```js
const express = require('express')

const app = express() 


// 配置使用 art-template 模板引擎
// 第一个参数表示，当渲染以.art结尾的文件的时候，使用art-template模板引擎
// express-art-template 是专门用来在Express 中 把art-template 整合到Express 中
// 虽然外面这里不需要加载art-template ,但是也必须要安装.
// 因为 express-art-template 依赖了art-template .

app.engine('art', require("express-art-template"))

// Express 为Response 相应对象提供了一个方法: render,
// render 方法默认是不可以使用,但是如果配置了模板引擎就可以使用.

// res.render('html模板名'， { 模板数据})

// 第一个参数不能写路径, 默认会去项目中的views 目录查找该模板文件.
// 也就是说Express 有一个约定: 开发人员把所有的视图文件都放到views目录中


app.get('/', function(req, res){
        res.render("404.art")
})


app.use('/a/', express.static('./public/'))


app.listen(3000, function(){
        console.log('running...')
})

```



### 总结：

```
app.get('/', function(req, res){
	// 默认会去项目中的views 目录查找该模板文件
        res.render('index.html',{    //这里吧index.html当做模板字符串。 {title}
			title:' hello world'
		})
})

```

### 修改默认路径

如果希望修改默认的`views` 视图渲染存储目录,可以

```
//注意：第一个views 不要写错
app.set('views', 目录路径)

比如；
app.engine('html', require("express-art-template")) //  渲染后缀是.html文件。
app.set('views', path.join(__dirname,'./views/'))  //默认查找views中 html 渲染
```





## 

# MongoDB 数据库

MongoDB 是由C++语言编写的，是一个基于分布式文件存储的开源数据库系统。

##   1  关系型数据库和菲关系型数据库

表 就是关系

或者说是表与表之间存在的关系

##  1.2 所有的关系型数据库特点：

1. 都需要通过`sql` 语言老操作

2. 在操作之前都需要设计表结构

3. 数据表还支持约束

   唯一的

   主键

   默认值

   非空

## 1.3 非关系型数据库特点：

灵活

有的非关系型数据库就是key- value对儿

## 1.4 MongoDB 

但是MongoDB  是长的最像关系型数据库和非关系型数据库

1. 其他  ==》 MongoDB 的

2. 数据库   ==》 数据库

3. 数据表   ==》 集合 或者是数组

4. 表记录   ==》文档对象

   MongoDB  不需要设计表结构

   也就是说可以任意的往里面存数据，没有结构性这么一说

## 2.使用安装

 2.1 安装包https://www.mongodb.org/dl/win32/x86_64

   http://www.mongodb.org/dl/win32/x86_64

http://www.mongodb.org/dl/win32/i386

![1594142362350](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594142362350.png)

MongoDB Compass Community可视化工具   这个是可视化的版本

![1594232824711](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594232824711.png)

可视化的一版



![1594281878077](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594281878077.png)



注意： 安装包是。msi结尾。别下错了

环境变量  （上面

panth  双击弹窗下面这个框

![1594140346697](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594140346697.png)

版本 分类 ：选择社区服务器  演示 2008   3.4.10      一路next 

 测试是否安装   mongod --version    

报错：bash: mongod: command not found  

原因是需要配置环境变量： 指令找不到执行文件，所以报错。

1.  找到安装包里面的bin 文件夹 复制路径  C:\Program Files\MongoDB\Server\3.4\bin

2.  找到电脑环境变量     -》 双击path 列   打开后 添加  ，复制进去路径，  点击确认。 （看上图）

3. 关闭cmd 命令行页面。 重新打开  测试 是否安装成功   完成

   ![1594142287057](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594142287057.png)

## 3.服务启动和关闭

3.1 https://www.runoob.com/mongodb/mongodb-window-install.html 菜鸟教程 win mongdb 安装 服务

3.2 另一种启动方法：

```
1. mongod默认使用执行mongod 命令所处盘符根目录下的/data/db  文件夹作为自己的数据存储目录
所以在第一次执行改名之前先自己手动新建一个 文件夹。
2. 命令行执行  mongod 启动成功   不要关闭控制台就是开启数据库  注意指令是 mongod

```

![1594143495314](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594143495314.png)

3. 关闭方法： ctrl + c   或者直接关闭控制台

## 4.连接数据库 和退出

另开一个控制台cmd

连接

```
输入 mongo   该命令是默认连接数据库
```

![1594235204041](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594235204041.png)

退出

```
输入：   exit
```

## 5.基本命令

```
1.   show  dbs  查看显示所有数据库    默认有admin  local 两个系统数据库，不要动
```

```
2. db   查看当前你操作的数据库     默认显示test  等到数据查库的时候，自动创建
```

```
3. use itcase(这是自己起的数据库名字)      切换指定数据库，没有的话自动创建
```

```
4. db.students.insertOne({'name':'jake'})   在itcase下 键值对形式 插库数据
```

```
show collections  显示集合
```

查看名字叫cats的数据库

```
db.cats.find（）  回车
```

在查看时会发现dbs ，会看到itcase 数据库。

## 在Node 中操作mongo数据库（使用node封装的插件 mongoose  ）

1.1 官方 有数据库操作文档   github  https://github.com/mongodb/node-mongodb-native

1.2 node 基于官方再次做了一次封装也开发了一版[mongoose](https://github.com/Automattic/mongoose)

 网址：  https://mongoosejs.com/

在npm插件的网站上可以可以找到安装方法

![1594144848849](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594144848849.png)

案例演示：

注意node的操作名字叫 mongo ose   

```js
官方demo
可以看出，node 把它当做插件引入，方法。所以使用准备工作：
1.新建文件夹
2.npm i
3.npm i mongoose
4. 打开cmd    输入  mongod  打开数据库，不要关闭 保持打开状态
5. 新建 js文件   下面代码
```

```js
// 引入包
const mongoose = require('mongoose');
//链接数据库
// 'mongodb://localhost:27017/test
//  mongodb数据库    本地地址   端口号  默认首个数据库名字 test
mongoose.connect('mongodb://localhost:27017/test', {useNewUrlParser: true, useUnifiedTopology: true});


//创建一个模型
//就是在设计数据库
//monggdb 是动态的，非常灵活， 只需要在代码中设计你的数据库就可以了
//mongoose  node封装的包，可以燃尽的设计编写过程变得非常简单
const Cat = mongoose.model('Cat', { name: String })
// 数据库名字 Cat， 首字母大写， 默认插库时转换为小写，加上s 复数。

// 实例化一个Cat
const kitty = new Cat({ name: 'Zildjian' });//Zildjian 是cat数据库中 集合名字

//持久化保存kitty实例

// 老版本写法： 
// kitty.save(function (err) {
//     if(err){
//         console.log(err);
        
//     }else{
//         console.log('neow');
        
//     }
// })
// 新版本写法： 
kitty.save().then(() => console.log('meow'));
```

6.   打开 git besh命令 执行js文件

```shell
$ node demo1.js
meow  //喵喵

```

另外开一个 cmd：

输入 mongo   该命令是默认连接数据库

```
> db
test
> show dbs
admin  0.000GB
local  0.000GB
> show dbs
admin  0.000GB
local  0.000GB
test   0.000GB
> db
test
> db.cats.find()
{ "_id" : ObjectId("5f0619862f0f3d29d0e4018b"), "name" : "Zildjian", "__v" : 0 }
```

{ "_id" : ObjectId("5f0619862f0f3d29d0e4018b"), "name" : "Zildjian", "__v" : 0 }

### 2.数据格式概念

MongoDB数据库的基本概念

虽然灵活，但还是要一定的规则创建数据结构。

1.可以有多个库

2. 一个数据库中可以有多个集合或 表

3. 一个集合中可以有多个文档（表记录）

4. 文档结构部很灵活，没有任何限制

5. Mongdb非常灵活，不需要想MySOl一样先创建数据库，表，设计表结构

   这里只需要：当你需要插入数据的时候，只需要指定往哪个数据库哪个集合操作就可以了

   一切都由MongDB来帮你自动完成建库 建表的事情。

```
{
qq: {
    users：
    [{name:'张三'，age：15},
    {name:'张三'，age：15},
    {name:'张三'，age：15}
    ]
},
weixin: {
    users：
    [{name:'张三'，age：15},
    {name:'张三'，age：15},
    {name:'张三'，age：15}
    ]
}
baidu: {
    users：
    [{name:'张三'，age：15},
    {name:'张三'，age：15},
    {name:'张三'，age：15}
    ]
}
}
```

### 3. 实例：

#### 3.1 文档配置

```
// 1. 引入包
const mongoose = require('mongoose');
// 2.引入数据数据模型
var Schema = mongoose.Schema;
// 3.链接数据库
mongoose.connect('mongodb://localhost:27017/test', {
    useNewUrlParser: true,
    useUnifiedTopology: true
});



// 规定数据结构  以保证数据的完整性，让数据保持一致。
//设计集合结构（表结构）
//字段名称就是表结构中的属性名称

var userSchema = new Schema({
    username: {
        type: String,
        required: true //必须有
    },
    password: {
        type: String,
        require: true
    },
    email: {
        type: String
    }
});


// mongoose.model方法就是用来将一个架构发布为model
// 第一个参数：传入一个大写的名词单数，字符串，用来表示你的数据库名称。
//    mongoose会自动将大写名词的字符串生成小写附属的集合名称
//      例如这里的User,最终会变成users集合名称。
//   第二个参数：架构Schema
//   返回值：模型构造函数   

const User = mongoose.model('User', userSchema)


// 4. 当我们有了模型构造函数之后，就可以使用这个构造函数对users集合总数据，进行处理了。


```

#### 3.2 添加数据

```
var admin = new User({
username:'lyx',
password:'123456',
email:'admin@admin.com'
})

admin.save(function(err ,ret){

    if (err) {
        console.log('保存失败');
        
    } else {
        console.log('保存成功');
        console.log(ret);

    }
})



```

```shell
$ node demo2.js
保存成功
{ _id: 5f062498263e94312cf2d2a8,
  username: 'lyx',
  password: '123456',
  email: 'admin@admin.com',
  __v: 0 }
```

```
> db.users.find()
{ "_id" : ObjectId("5f062498263e94312cf2d2a8"), "username" : "lyx", "password" : "123456", "email" : "admin@admin.com", "__v" : 0 }
```

#### 3.3 查询 数据

所有all

```
User.find(function(err ,ret){

    if (err) {
        console.log('保存失败');
        
    } else {
        console.log('保存成功');
        console.log(ret);

    }
})
```

#### 3.3 条件查询

```
User.find({
    username:'tom'   //传入一个对象
},function(err ,ret){

    if (err) {
        console.log('查询失败');
        
    } else {
        console.log('查询成功');
        console.log(ret);

    }
})

```

查询第一个符合条件的

```
User.findOne({
    username:'tom'   //这一个可以不加  条件可以多个
},function(err ,ret){

    if (err) {
        console.log('查询失败');
        
    } else {
        console.log('查询成功');
        console.log(ret);

    }
})

// 查询不到： null
```

#### 3.4 删除数据

```
// User.remove({
//     username:'tom'   //这一个可以不加  条件可以多个
// },function(err ,ret){

//     if (err) {
//         console.log('查询失败');
        
//     } else {
//         console.log('查询成功');
//         console.log(ret);

//     }
// })

```

#### 3.5 更新数据

```
User.findByIdAndUpdate('5f0626dd6dd8ea3ff011c456',{
    password: '123'

},function(err ,ret){

    if (err) {
        console.log('修改失败');
        
    } else {
        console.log('修改成功');
        console.log(ret);

    }
})



```



# 案例

```
var mongoose = require('mongoose')

var Schema = mongoose.Schema;

mongoose.connect('mongodb://localhost:27017/lyx-test', {
    useNewUrlParser: true,
    useUnifiedTopology: true
});


var studentSchema = new Schema({

    name: {
        type: String,
        required: true //必须有
    },
    gender: {
        type: Number,
        enum:[0,1],
        default:0
    },
    age: {
        type: Number
    },
    hobbies: {
        type: String
    }
});


const User = mongoose.model('User', userSchema)


```

数据库创建和查询 完整代码

````javascript
// 1. 引入包
const mongoose = require('mongoose');
// 2.引入数据数据模型
var Schema = mongoose.Schema;
// 3.链接数据库
mongoose.connect('mongodb://localhost:27017/test', {
    useNewUrlParser: true,
    useUnifiedTopology: true
});



// 规定数据结构  以保证数据的完整性，让数据保持一致。
//设计集合结构（表结构）
//字段名称就是表结构中的属性名称

var userSchema = new Schema({

    username: {
        type: String,
        required: true //必须有
    },
    password: {
        type: String,
        require: true
    },
    email: {
        type: String
    }
});


// mongoose.model方法就是用来将一个架构发布为model
// 第一个参数：传入一个大写的名词单数，字符串，用来表示你的数据库名称。
//    mongoose会自动将大写名词的字符串生成小写附属的集合名称
//      例如这里的User,最终会变成users集合名称。
//   第二个参数：架构Schema
//   返回值：模型构造函数   

const User = mongoose.model('User', userSchema)
console.log(User.find,'this');

// 4. 当我们有了模型构造函数之后，就可以使用这个构造函数对users集合总数据，进行处理了。

// 插入数据
// var admin = new User({
// username:'tom',
// password:'123456',
// email:'admin@admin.com'
// })

// admin.save(function(err ,ret){

//     if (err) {
//         console.log('保存失败');
        
//     } else {
//         console.log('保存成功');
//         console.log(ret);

//     }
// })


// 查询数据 all

// User.find({
//     username:'tom'
// },function(err ,ret){

//     if (err) {
//         console.log('查询失败');
        
//     } else {
//         console.log('查询成功');
//         console.log(ret);

//     }
// })

// 查询数据   条件查询

// User.find({
//     username:'tom'
// },function(err ,ret){

//     if (err) {
//         console.log('查询失败');
        
//     } else {
//         console.log('查询成功');
//         console.log(ret);

//     }
// })

// 查询数据   符合条件的第一个数据

// User.findOne({
//     username:'tom'   //这一个可以不加  条件可以多个
// },function(err ,ret){

//     if (err) {
//         console.log('查询失败');
        
//     } else {
//         console.log('查询成功');
//         console.log(ret);

//     }
// })

// 查询不到： null


// 删除数据

// User.remove({
//     username:'tom'   //这一个可以不加  条件可以多个
// },function(err ,ret){

//     if (err) {
//         console.log('查询失败');
        
//     } else {
//         console.log('查询成功');
//         console.log(ret);

//     }
// })

// 更新数据
// https://mongoosejs.com/docs/api/model.html
// Model.findOneAndUpdate()
// Model.updateMany()
// Model.updateOne()
// Model.findByIdAndUpdate()


User.findByIdAndUpdate('5f0626dd6dd8ea3ff011c456',{
    password: '123'

},function(err ,ret){

    if (err) {
        console.log('修改失败');
        
    } else {
        console.log('修改成功');
        console.log(ret);

    }
})


User.find(function(err ,ret){

    if (err) {
        console.log('查询失败');
        
    } else {
        console.log('查询成功');
        console.log(ret);

    }
})
````







# 博客数据库使用记录：

mongdb数据库使用前提；

1.  是  node命令先打开， 
2.  查看数据库： 线连接 ，再查找命令。



mongoose  是node封装的 操作罗 mongdb数据库的插件。



安装插件：





