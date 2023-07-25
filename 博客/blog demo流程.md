# blog demo流程

记录一个node.js项目用到的所有的技术栈

## 1 . 项目 目录结构

1.1   初始化一个package.json 文件 记录包的信息

```javascript
 npm init -y   
```

1.2    初始化一个git本地仓库   

```
 git init     用于发布到github上准备文件夹中出现一个  .git文                件  记录git信息
```

1.3     新建README.md项目自述文件      （read me 读我）

```
  上传时， git上会显示出来。
```

1.4 建立git 忽略文件   ignore（忽略）



```
.gitignore 文件夹 

作用是： 记录那些文件不需要上传到github上。 上传时，忽略
```

1. 5  引入配置项 插件



```
npm i express mongoose     一个是操作node 开发框架 一个是操作数据库
```

1.6 建立项目中共开文件 public

```
public--|
        |---css
        |---js
        |---img
```

1.7 新建 app.js 入口 js文件

1.7.1 开放路径

```
 项目启动入口
 var express = require('express')

var path = require('path')   // 路径操作模块

var app = express()

app.use('/public/' ,express.static(path.join(__dirname,'./public/'))) //path.join 相对- > 绝对路径

// 测试： http://127.0.0.1:5000/node_modules/accepts/index.js   浏览器可以访问到文件

app.use('/node_modules/' ,express.static(path.join(__dirname,'./node_modules/')))

app.engine('html', require("express-art-template"))
app.set('views', path.join(__dirname,'./views/'))

app.get('/', function(req, res){
	// 默认会去项目中的views 目录查找该模板文件
        res.render('index.html',{    //这里吧index.html当做模板字符串。 {title}
			title:' hello world'
		})
})

// app.get('/', function(req, res){

//     res.send('hello')

// })

app.listen(5000, function(){
console.log('running...');
  
})

```

1.8 引入模板template

```
npm install --save art-template
npm install --save express-art-template     两个都加载， 有相互依赖关系。
```



## 2.补充知识：

##### node.js中的两个非模块成员   动态获取

__dirname  可以用来获取当前文件模块所属的绝对路径

__filename  可以用来获取当前文件模块所属的相对路径

为什么官方设置这个参数

```
console.log(__dirname);

console.log(__filename);


./a.txt 这里的路径，当前，指的是 node命令进入的文件的，当前。 node中相对路径不可靠，所以才转换绝对路径
fs.readFile('./a.txt','utf8',function(err ,data){

})

node中的文件路径， 是相对与命令行所在文件，作为参考对象。
即： node命令行 在C:/   执行文件。 fs.readFile('./a.txt', 。。。  默认是在c:/a.txt 执行。没有就报错 
```

使用方式： 直接使用，不用引入插件。

## 3.tem-plate的方法

#### 3.1公共头部

![1594533063685](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594533063685.png)

index.html

```
<body>
    {{include './header.html'}}  //填入路径
    {{title}}
    {{include './footer.html'}}
</body>
```

header.html

```
<div class="header">
    <h1>我是heaer</h1>
</div>
```

![1594533104263](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594533104263.png)

#### 3.2模板继承

layout.html  index.html 在同一文件夹内

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    {{ block 'css' }}  {{ /block}} 1. 为自定义 css留坑
    
</head>

<body>
    {{include './header.html'}}
    
    {{block 'content'}}  // 2. 备用坑位
    <h1>默认内容</h1>
    {{/block}}
    
    {{include './footer.html'}}
    
 {{ block 'script' }}  {{ /block}} 3. 为自定义 js留坑
</body>

</html>
```



##### index.html  引入自己的内容

```
{{extend './layout.html'}}    //就写这一个   扩展  + 路径


填入index自己的内容

{{extend './layout.html'}}





1. 替换为自己的css   
{{block 'css'}}
<style>
body{
    background-color:red
}
</style>
{{/block}} 


{{block 'content'}}   // 2. 替换自己的内容
<div>
    <h1>我是index内容</h1>
</div>
{{/block}}


{{block 'script'}}  //3. js模板会把坑位的标签， 替换为  block 'script' 中的内容

<script>

console.log(0)

</script>

{{/block}} 
```

## 4.目录设计

```
.
|—— app.js
|—— controllers
|—— models            数据库的   数据模型
|—— node_modules       第三方包
|—— packgge.json       包的描述文件
|—— packgge-lock.json   第三方版本错锁定文件（npm5以后才有）
|—— public            公共静态资源
|—— README.md         项目说明文档
|——  routes     路由
|—— views      存储视图目录
|—— 
|—— 

```



## 5.路由设计

| 路径      | 方法 | get 参数 | post参数                  | 是否需要登录 | 备注         |
| --------- | ---- | -------- | ------------------------- | ------------ | ------------ |
| /         | GET  |          |                           |              | 渲染首页     |
| /register | GET  |          |                           |              | 渲染注册页   |
| /register | POST |          | email, nickname, password |              | 处理注册请求 |
| /login    | GET  |          |                           |              | 渲染登录页   |
| /login    | POST |          | email, password           |              | 处理登录请求 |
| /logout   | GET  |          |                           |              | 处理退出请求 |

###### 

## 6. router.js 路由分离

```
var express = require('express')

var router = express.Router()

router.get('/', function (req, res) {
    res.render('index.html')
})

```

## 7. 配置body-parser请求体插件

```
$ npm install body-parser


var bodyParser = require('body-parser')// 1.先引入包


app.use(bodyParser.urlencoded({ extended: false }))  //配置表单解析post请求体插件，一定放到                                                           //app.use(router)之前
app.use(bodyParser.json()) 



req.body
```

## 8. Express响应的方法：res.status(200).json（{}）

关于数据转换的问题

后端

```
router.post('/register', function (req, res) {
    // console.log(req.body);
    // 2. 操作数据库
    // 判断用户是否存在 
    //存在，不允许注册
    // 不存在，注册新建用户
    //3. 发送响应
    var body = req.body

    User.findOne({
        $or: [{ //或语句  查看文档 或者是菜鸟教程
            email: body.email
        }, {
            nickname: body.nickname
        }]

    }, function (err, data) {
        if (err) {
           
            return res.status(500), send('emaill  err')
        }

        if (data) {
            return res.status(200), send('emaill or nickname aleary exists')
        }
        res.status(200).send('{"success":true}')    ====看这里send('ok')    发送ok ，ajax尝试把ok转化为json, 不会报错。
    })
})


或者是    先转换，再返回
 res.status(200).send(JSON.stringify({
            success:true
        }))

// Express提供一个响应的方法： json ; 方法接受一个对象作为参数。 作用是把对象自动转为字符串，并返回前端。
res.status(200).json({
    success:true,
    foo:'bar'
})

```



```
  $('#register_form').on('submit', function (e) {
      e.preventDefault()
      var formData = $(this).serialize()
      $.ajax({
        url: '/register',
        type: 'post',
        data: formData,
        dataType: 'json',                  //上面如果返回的是不是json形式的字符串，ajax接受不到
        success: function (data) {
          console.log(data);                 //上面如果
          var err_code = data.err_code
          if (err_code === 0) {
            // window.alert('注册成功！')
            // 服务端重定向针对异步请求无效
            window.location.href = '/'
          } else if (err_code === 1) {
            window.alert('邮箱已存在！')
          } else if (err_code === 2) {
            window.alert('昵称已存在！')
          } else if (err_code === 500) {
            window.alert('服务器忙，请稍后重试！')
          }
        }
      })
    })
```

## 9.安装node - MD5 密码加密

https://github.com/blueimp/JavaScript-MD5

```
npm install blueimp-md5  

var md5 = require('blueimp-md5')
var pasword = md5(pasword)

```



## 10. 第三方中间件cookie    

#### EditThisCookie  插件  查看 express cookies状态值

```
// 在Express 这个框架中，默认不支持Session 和cookie，但是我们可以使用第三方中间件
// express-session来解决。
// 1. npm install express-session
// 2. 配置  var session = require('express-session')

3. 设置中间件  
  app.use(session({
  secret: 'keyboard cat',
  resave: false,
  saveUninitialized: true
}))


//  4）使用

            设置值 req.session.username=“lhj”

            获取值 req.session.username
值挂载到req 请求中。
例如：
router.get('/register', function (req, res) {

    res.render('register.html')
    req.session.isvip= true
console.log(req.session);
})

打印值：
Session {
  cookie:
   { path: '/',
     _expires: null,
     originalMaxAge: null,
     httpOnly: true },
  isvip: true }

```

11 服务器与前端的交互实质就是字符串的交互