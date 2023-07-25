Express中间件

## 中间件的概念

> 参考文档：http://expressjs.com/en/guide/using-middleware.html

![1594703709264](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594703709264.png)

中间件：把很复杂的事情分割成单个，然后依次有条理的执行。就是一个中间处理环节，有输入，有输出。

说的通俗易懂点儿，中间件就是一个（从请求到响应调用的方法）方法。

把数据从请求到响应分步骤来处理，每一个步骤都是一个中间处理环节。

```javascript
var http = require('http');
var url = require('url');

var cookie = require('./expressPtoject/cookie');
var query = require('./expressPtoject/query');
var postBody = require('./expressPtoject/post-body');

var server = http.createServer(function(){
	// 解析请求地址中的get参数
	// var obj = url.parse(req.url,true);
	// req.query = obj.query;
	query(req,res);	//中间件
	
	// 解析请求地址中的post参数
	req.body = {
		foo:'bar'
	}
});

if(req.url === 'xxx'){
	// 处理请求
	...
}

server.listen(3000,function(){
	console.log('3000 runing...');
});
```

同一个请求对象所经过的中间件都是同一个请求对象和响应对象。

```javascript
var express = require('express');
var app = express();
app.get('/abc',function(req,res,next){
	// 同一个请求的req和res是一样的，
	// 可以前面存储下面调用
	console.log('/abc');
	// req.foo = 'bar';
	req.body = {
		name:'xiaoxiao',
		age:18
	}
	next();
});
app.get('/abc',function(req,res,next){
	// console.log(req.foo);
	console.log(req.body);
	console.log('/abc');
});
app.listen(3000, function() {
	console.log('app is running at port 3000.');
});

```

![image-20200317110520098](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200317110520098.png)

## 中间件的分类:

### 应用程序级别的中间件

万能匹配（不关心任何请求路径和请求方法的中间件）： 过滤所有的请求路径

```javascript
app.use(function(req,res,next){
    console.log('Time',Date.now());
    next();
});
```

关心请求路径和请求方法的中间件：               匹配过滤

```javascript
app.use('/a',function(req,res,next){
    console.log('Time',Date.now());
    next();
});
```

### 路由级别的中间件

严格匹配请求路径和请求方法的中间件      严格匹配过滤

get:

```javascript
app.get('/',function(req,res){
	res.send('get');
});
```

post：

```javascript
app.post('/a',function(req,res){
	res.send('post');
});
```

put:

```javascript
app.put('/user',function(req,res){
	res.send('put');
});
```

delete:

```javascript
app.delete('/delete',function(req,res){
	res.send('delete');
});
```

### 总

```javascript
var express = require('express');
var app = express();

// 中间件：处理请求，本质就是个函数
// 在express中，对中间件有几种分类

// 1 不关心任何请求路径和请求方法的中间件
// 也就是说任何请求都会进入这个中间件
// 中间件本身是一个方法，该方法接收三个参数
// Request 请求对象
// Response 响应对象
// next 下一个中间件
// // 全局匹配中间件
// app.use(function(req, res, next) {
// 	console.log('1');
// 	// 当一个请求进入中间件后
// 	// 如果需要请求另外一个方法则需要使用next（）方法
// 	next();
// 	// next是一个方法，用来调用下一个中间件
//  // 注意：next（）方法调用下一个方法的时候，也会匹配（不是调用紧挨着的哪一个）
// });
// app.use(function(req, res, next) {
// 	console.log('2');
// });

// // 2 关心请求路径的中间件
// // 以/xxx开头的中间件
// app.use('/a',function(req, res, next) {
// 	console.log(req.url);
// });

// 3 严格匹配请求方法和请求路径的中间件
app.get('/',function(){
	console.log('/');
});
app.post('/a',function(){
	console.log('/a');
});

app.listen(3000, function() {
	console.log('app is running at port 3000.');
});

```

## 错误处理中间件

```javascript
app.use(function(err,req,res,next){
    console.error(err,stack);
    res.status(500).send('Something broke');
});
```

配置使用404中间件：

```javascript
app.use(function(req,res){
    res.render('404.html');
});
```

配置全局错误处理中间件:

当有next() 有参数时， 会直接跳过中间的过滤，找到有4个参数的中间件（这最后一个就是全局错误中间件），执行。

一般为了代码的简介，可以在最后配置一个全局错误中间件。

```javascript
app.get('/a', function(req, res, next) {
	fs.readFile('.a/bc', funtion() {
		if (err) {
        	// 当调用next()传参后，则直接进入到全局错误处理中间件方法中
        	// 当发生全局错误的时候，我们可以调用next传递错误对象
        	// 然后被全局错误处理中间件匹配到并进行处理
			next(err);
		}
	})
});
//全局错误处理中间件
app.use(function(err,req,res,next){
    res.status(500).json({
        err_code:500,
        message:err.message
    });
});
```

## 同一个请求，req,res是同一个



```
app.get('/abc',function(req,res,nextt){
	req.body = {}
});

app.get('/abc',function(req,res,nextt){
	console.log(req.body)  在这里可以拿到上面变量加进去的值
});

这就是为什么app.use（） ，之前挂载方法的原因。


```



## 内置中间件

- express.static(提供静态文件)
  - http://expressjs.com/en/starter/static-files.html#serving-static-files-in-express

## 第三方中间件

> 参考文档：http://expressjs.com/en/resources/middleware.html

- body-parser
- compression
- cookie-parser
- mogran
- response-time
- server-static
- session

