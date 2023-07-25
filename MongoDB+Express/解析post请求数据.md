## 解析post请求数据

http://expressjs.com/en/starter/static-files.html   官网上

使用插件的原因： 

1.  req.query 注意： query只能拿到get  通过url传递的数据。 post 不是通过路径传参,

在Express中没有内置获取表单post请求体的API, 这里我们需要使用一个第三方包： `body-parser`



## Installation 安装

```js
$ cnpm install body-parser
```

## API

```
var bodyParser = require('body-parser')
```

案例

```js
var express = require('express')
var bodyParser = require('body-parser')// 1.先引入包

var app = express()
  //配置body-parser
//只要加入这个配置，则在req请求对象上，会多出来一个属性：body
//也就是说你可以直接通过 req.body 来获取变淡post请求体数据了、

// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))  //2. use往app上添加方法
// parse application/json
app.use(bodyParser.json())                //2. use往app上添加方法

app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  res.end(JSON.stringify(req.body, null, 2))   //3. req.body 获取数据
})
```

补充：  浏览器输入地址 敲回车，永远是get请求。  post请求方式 ：1. table表格提交， 2.Ajax请求发起