# nginx代理

实测记录：

本地部署时，关于root路径出现问题，无法访问到资源。

解决： win系统下盘符内 ，/ 正斜杠        \反斜杠 路径不行。

```
        location / {
           # root  html;   <---原来
              root  "F:/testdemo/dist";   <---我的本地电脑
            index  index.html index.htm;
        }
       location /prod-api/ {
				proxy_set_header Host $http_host;
				proxy_set_header X-Real-IP $remote_addr;
				proxy_set_header REMOTE-HOST $remote_addr;
				proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
				proxy_pass http://192.168.112.4:8888/;
            }
```

 

排查问题思路：

1 当修改了config配置文件，先nginx -t 检查一下语法。  （能检查的一部分错误）

2.启动服务，查看报错日志。  （会提示报错的  专有报错码）

   下面是一个路径错误。  

  location / {

​      root  F:\testnginx\dist;                                          win下   左斜杠两个，右斜杠可以用一个。 

​      index  index.html index.htm;

​    }

```
2025/11/06 10:31:43 [crit] 21948#20588: *1 GetFileAttributesEx() "F:	estnginx\dist" failed (123: The filename, directory name, or volume label syntax is incorrect), client: 127.0.0.1, server: localhost, request: "GET / HTTP/1.1", host: "127.0.0.1"  分析日志
```

这条日志的核心问题是 **路径语法错误**，和你之前日志中反复出现的报错根源完全一致，具体分析和修复步骤如下：

### 一、日志关键信息拆解

| 字段                                       | 含义                                                         |
| ------------------------------------------ | ------------------------------------------------------------ |
| `[crit]`                                   | 严重错误（路径语法完全无法识别，Nginx 无法执行文件查找操作） |
| `GetFileAttributesEx() "F: estnginx\dist"` | Nginx 尝试获取路径属性，但路径被解析错误：`F:\testnginx\dist` 变成了 `F: estnginx\dist`（`\t` 被识别为制表符） |
| `(123: 语法不正确)`                        | Windows 系统的路径语法错误码，直接原因是 **单个反斜杠 `\` 被解析为转义字符** |
| `request: "GET / HTTP/1.1"`                | 访问根路径 `/` 时触发，说明 `nginx.conf` 中 `root` 配置的路径存在语法问题 |



win下正确的配置

```
root  F:/testnginx/dist; 
```



******************************************************************

官网下载

https://nginx.org/

https://nginx.org/en/download.html  下载页面

### 一，Nginx是什么，适用场景？

**1，http的反向代理服务器**

**正向代理**：给客户端用的。客户端先发送请求到[代理服务器](https://so.csdn.net/so/search?q=代理服务器&spm=1001.2101.3001.7020)，然后通过代理服务器转发给所请求的服务器。

反向代理：给服务端用的。客户端去访问的时候，不直接访问到所要请求的服务器，而是在这个服务器前面统一加一个服务器，这个服务器会把内容进行合理的转发和返回。

**反向代理**服务器主要作用：

提供安全性，比如防火墙。

在后端多个服务器里提供负载均衡，这样就能充分利用服务器资源。

提供缓存。有的时候服务器处理速度比较慢，可以把常用内容存到服务器缓存代理服务器，这样后续用户请求时候可以直接从反向代理服务器里面去取。
原文链接：https://blog.csdn.net/qq_36792120/article/details/115421572

**同时使用正向+反向代理**

2，动态静态资源分离，提高运行速度

动态静态资源不会离会变慢（静态：图片，css之类。动态：具体的逻辑请求啥的）

静态资源无需经过tomcat，tomcat只负责处理动态请求

后缀为gif的时候，nginx会直接获取到当前请求的文件并返回

eginx本身也是一个静态资源服务器，比如我们只有静态资源的时候，比如个人主页等可以作为静态资源网站去实现，开发的时候可以直接把eginx当做一个服务器，无需安装tomcat，而且eginx性能也不错


### 二，eginx的优点

高并发，高性能：32G+64G主流服务器的配置，使用eginx可以轻松达到千万级别的并发

可扩展性好：主要体会在模块化设计非常稳定，所以三方模块生态圈非常丰富

高可靠性：可以在服务器可靠不间断运行长达数年，不需要进行重启维护

热部署：可以在不停止服务的情况下去升级eginx

开源，可商用

## 三，常用命令

命令	作用
/usr/sbin/nginx	启动
再次输入启动命令 / ps -aux|grep nginx / 浏览器输入网站看下能否访问成功	验证是否启动
nginx -h	帮助
nginx -c	读取指定配置文件 ，比如 eginx -c /etc/nginx/nginx.conf
nginx -s stop	关闭eginx
nginx -t	测试配置文件是否正确
nginx -v	打印版本号
nginx -V	打印版本号，编译器，配置参数等其他配置信息
ps aux | grep eginx	找到eginx所在路径
nginx -s stop	立即停止（不管不顾）
nginx -s quit	优雅停止（旧的进程收到命令，在此刻就停止链接，可能在此之前已经请求过来的，会继续提供服务直到服务完毕，没有新的内容需要处理了，再进行退出，线上推荐这种！！）
nginx -s reload	重启（收到重启命令后，检查新的配置文件的语法有效性，如果语法有问题不会重启。如果检查通过会启动新进程。直到旧的进程把它已经拥有的命令处理完毕后再退出旧的进程）
eginx -s reopen	更换日志文件



## 四，语法

1. ; 结尾
2. {}组织多条指令
3. include引入（比如配置多个端口号，配置完成后用include /etc/nginx/conf.d/*.conf；进行加载，逻辑会非常清晰）
4. \# 注释
5. $ 变量



执行命令

进入nginx插件所在文件夹

```
D:\nginx-1.4.7\
```

运行以下命令检查Nginx配置文件的语法是否正确：

win服务器演示：

```
nginx -t
```



案例：

```java

#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;
 
    server {
             listen       8007;
             server_name  192.168.112.3;

             location / {
                   root D:\WebProject\erligang;
				   try_files $uri $uri/ /index.html;
                   index index.html index.htm;
             }
			
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }


	 server {
             listen       8018;
             server_name  192.168.112.3;
			 charset utf-8;
			 
             location / {
                   root D:\WebProject\shanghai-pipe;
				   try_files $uri $uri/ /index.html;
                   index index.html index.htm;
             }
			 
			 location /prod-api/ {
				proxy_set_header Host $http_host;
				proxy_set_header X-Real-IP $remote_addr;
				proxy_set_header REMOTE-HOST $remote_addr;
				proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
				proxy_pass http://192.168.112.2:8080/;
            }
			
			  location ~ /RPC2|RPC2_Login|RPC_Loadfile/ {
            proxy_pass http://$http_self_targetip;
            break;
        }	
        
        location ^~ /web_caps/ {
            proxy_pass http://$http_self_targetip;
            break;
        }	


			 
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
	
		server {
             listen       8021;
             server_name  192.168.112.3;
			 charset utf-8;
			 
             location / {
                   root D:/WebProject/three-lab;
				   try_files $uri $uri/ /index.html;
                   index index.html index.htm;
             }
			 
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }

    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443;
    #    server_name  localhost;

    #    ssl                  on;
    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_timeout  5m;

    #    ssl_protocols  SSLv2 SSLv3 TLSv1;
    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers   on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}

```



## 实测指令 

### 1.下载

稳定版本 以nginx/Windows-1.18.0为例

### 2 打开命令工具

进入nginx所在目录，输入cmd 打开命令工具。

### 3.开启服务：

(1)直接双击nginx.exe，双击后一个黑色的弹窗一闪而过
（注意如果点击多次，会启动很多个，导致使用nginx -s stop无法关闭完全）

输入命令 **nginx.exe** 或者 **start nginx** ，回车即可

### 4.检查端口是否被占用

```
netstat -ano | findstr 0.0.0.0:80
```

### 5.检查nginx是否启动成功

直接在浏览器地址栏输入网址 http://localhost:80，回车，出现以下页面说明启动成功

### 6.刷新配置

当我们修改了nginx的配置文件nginx.conf 时，
不需要关闭nginx后重新启动nginx，只需要执行命令 **nginx -s reload** 即可让改动生效

nginx.exe -s reload 重载nginx服务，当你改变了nginx配置信息并需要重新载入这些配置时可以使用此命令重载nginx

注意点：80端口是nginx的默认端口，也就是说，在没有加端口时，默认80.

  http://localhost/haochi   等同于  http://localhost:80/haochi

### 7.关闭nginx

如果使用cmd命令窗口启动nginx，关闭cmd窗口是不能结束nginx进程的，可使用两种方法关闭nginx

(1)输入nginx命令  **nginx -s stop** (快速停止nginx) 或 nginx -s quit(完整有序的停止nginx)

nginx.exe -s stop 关闭nginx服务，快速停止nginx，可能并不保存相关信息

nginx.exe -s quit 关闭nginx服务，完整有序的停止nginx，并保存相关信息

(2)使用taskkill taskkill /f /t /im nginx.exe

### 8.nginx命令参数v与V的区别

nginx -v命令只是简单显示nginx的版本信息(nginx version)

nginx -V不但显示nginx的版本信息，而且还显示nginx的配置参数信息。



### .bat快捷插件

![](https://i-blog.csdnimg.cn/blog_migrate/feceee8b859b3d905e1dab0c92846120.png)

与nginx脚本搭配使用的神器， -->RunHiddenConsole 

[详见](https://blog.csdn.net/gitblog_00093/article/details/139850656)，主要功能是，避免控制台频繁弹出，保持界面清爽。

准确的叫法为：批处理文件

在DOS,OS/2和[微软](https://baike.baidu.com/item/微软/124767?fromModule=lemma_inlink)Windows操作系统中，[批处理文件](https://baike.baidu.com/item/批处理文件/5363369?fromModule=lemma_inlink)(batch file)是包含一系列命令的文本文件，由命令[解释器](https://baike.baidu.com/item/解释器/10418965?fromModule=lemma_inlink)[解释执行](https://baike.baidu.com/item/解释执行/8081777?fromModule=lemma_inlink)。批处理文件是一种简单的程序，可以通过条件语句(if)和流程控制语句(goto)来控制命令运行的流程，在[批处理](https://baike.baidu.com/item/批处理/1448600?fromModule=lemma_inlink)中也可以使用循环语句(for)来循环执行一条命令 。

#### 如何只做一个批处理文件执行任务

以下是一个示例的批处理文件（假设Nginx已经安装在你的电脑上，并且其可执行文件位于 `C:\nginx\nginx.exe`）：

```
@echo off
echo Starting Nginx...
C:\nginx\nginx.exe
echo Nginx started successfully.
pause
```

1. 打开文本编辑器（如记事本）。
2. 将上述代码复制并粘贴到文本编辑器中。
3. 保存文件，确保文件名以 `.bat` 结尾，例如 `start_nginx.bat`。
4. 双击该批处理文件，或者从命令提示符中运行它，来启动Nginx。

注意：

- 你需要确保Nginx的安装路径是正确的。如果Nginx安装在不同的位置，你需要相应地修改批处理文件中的路径。

- `pause` 命令会暂停脚本的执行，并显示一个消息，等待用户按任意键继续。这可以让你在命令提示符窗口中看到Nginx的启动消息。如果你不希望这样做，可以删除 `echo Nginx started successfully.` 和 `pause` 这两行。

- 如果你想要停止Nginx，你可以使用类似的批处理文件，但使用 `nginx.exe -s stop` 命令。

  

## nginx的root配置

https://blog.51cto.com/u_16213592/11128152

Win10环境中Nginx配置文件中server里root该配置什么路径 nginx的root配置

root指令
ro0t指令在Nginx配置中非常常见，用于设置服务器中资源的根目录。这意味着Nginx会从这个指定的目录中查找并服务文件。

root与alias的主要区别
路径拼接方式:使用root时，location块中指定的URI将会直接拼接到r0o路径后面，而alias则会将location中匹配的部分路径替换为alias指定的路径
适用场景:root适用于网站的广泛区域，常在server或location块中定义，alias适用于单独改变特定location的路径，适合更细粒度的路径控制,

注意:
1.使用alias时，目录名后面一定要加"/"
2.alias在使用正则匹配时，必须捕捉要匹配的内容并在指定的内容处使用3.alias只能位于location块中。(root可以不放在location中)

使用场景
·使用root:当你想为整个服务器或者特定位置提供一个统一的根目录时，使用root是最简单直接的方法。
。使用alias:当你需要对服务器上的特定资源进行映射，而这部分资源又不在当前的根目录中时，alias是不可或缺的。例如，如果某些动态生成的文件存放在不同于静
态文件的目录，就可以通过alias来进行特殊处理。



