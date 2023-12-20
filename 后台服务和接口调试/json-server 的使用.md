# json-server 的使用

## 功能

json-server可以直接把一个json文件托管成一个具备全RESTful风格的API,并支持跨域、jsonp、路由订制、数据快照保存等功能的 web 服务器。

简单说：node启动服务，使用本地一个json文件，快速形成一个具备CRUD的接口服务。方面前台临时调试使用。

Json-server 是一个零代码快速搭建本地 RESTful API 的工具。它使用 JSON 文件作为数据源，并提供了一组简单的路由和端点，可以模拟后端服务器的行为。
github地址：https://github.com/typicode/json-server
npm地址：https://www.npmjs.com/package/json-server


## 环境准备

电脑已安装node ,配置环境变量。

## 创建工程

1. 创建工程目录(不要叫json-server)，如`D:\workspace\json-server-demo`，在工程目录下执行`npm init`，输入项目名、描述、作者(如果不输入就是默认的，直接回车)

2. 执行成功后，工程目录下会出现一个package.json文件

3. 继续执行`npm install json-server –save`安装json-server模块。–save就是将模块存储到package.json文件中

4.修改package.json  添加scripts指令

  ```
“json:server”: “json-server --watch db.json”
  ```

5.输入指令`npm run json:server`运行项目，命令中的“json:server”就是在package.json的scripts中配置的命令。

访问http://localhost:3000

## CRUD

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>删除数据</title>
    <script src="./jquery.min.js"></script>
</head>

<body>
    <button id="delete">删除数据</button>
    <script>

        //查询数据
        // $("#delete").click(function() {
        //     $.ajax({
        //         type: 'get',
        //         url: 'http://localhost:3000/articles',
        //         dataType: "json",
        //         success: function(data) {
        //             console.log("success",data)
        //         },
        //         error: function() {
        //             alert("delete error")
        //         }
        //     })
        // })
		//删除数据
		// $("#delete").click(function() {
		//     $.ajax({
		//         type: 'delete',
		//         url: 'http://localhost:3000/articles/2',
		//         dataType: "json",
		//         success: function(data) {
		//             console.log("delete success")
		//         },
		//         error: function() {
		//             alert("delete error")
		//         }
		//     })
		// })
		
	//添加数据
	// $("#delete").click(function() {
	//     $.ajax({
	//         type: 'post',
	//         url: 'http://localhost:3000/articles',
	//         dataType: "json",
	// 		data:{
	// 			userId: 6,
	// 			id: 52,
	// 			title: '添加数据',
	// 			body: '添加数据'
	// 		},
	//         success: function(data) {
	//             console.log("delete success",data)
	//         },
	//         error: function() {
	//             alert("delete error")
	//         }
	//     })
	// })
	//修改数据
	$("#delete").click(function() {
	    $.ajax({
	        type: 'put',
	        url: 'http://localhost:3000/articles/52',
	        dataType: "json",
			data:{
				userId: 6,
				// id: 52,
				title: '添加数据-修改了内容',
				body: '添加数据'
			},
	        success: function(data) {
	            console.log("delete success",data)
	        },
	        error: function() {
	            alert("delete error")
	        }
	    })
	})
    </script>
</body>

</html>

```

## 参数说明

语法：json-server [options] <source>
参数	简写	说明	默认值
–config	-c	指定配置文件路径	json-server.json
–port	-p	指定端口	3000
–host	-H	指定主机名	localhost
–watch	-w	监控文件变化	
–routes	-r	指定路由文件路径	
–middlewares	-m	指定中间件文件路径	
–static	-s	指定静态文件文件夹路径	
–read-only	–ro	指定只允许get请求	
–no-cors	–nc	禁止跨域共享	
–no-gzip	–ng	禁止gzip压缩	
–snapshots	-S	指定快照目录	.
–delay	-d	指定延迟返回时长(ms)	
–id	-i	指定数据库的ID属性	id
–foreignKeySuffix	–fks	指定外键前缀	Id
–quiet	-q	抑制来自输出的日志消息	
–help	-h	显示帮助	
–version	-v	显示版本号	
