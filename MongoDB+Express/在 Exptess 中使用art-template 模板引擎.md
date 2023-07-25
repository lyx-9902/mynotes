## 在 Exptess 中使用art-template 模板引擎

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



总结：

```
app.get('/', function(req, res){
	// 默认会去项目中的views 目录查找该模板文件
        res.render('index.html',{    //这里吧index.html当做模板字符串。 {title}
			title:' hello world'
		})
})

```

如果希望修改默认的`views` 视图渲染存储目录,可以

```
//注意：第一个views 不要写错
app.set('views', 目录路径)
```

