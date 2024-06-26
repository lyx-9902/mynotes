# nginx代理

官网下载

https://nginx.org/

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
eginx -h	帮助
eginx -c	读取指定配置文件 ，比如 eginx -c /etc/nginx/nginx.conf
eginx -s stop	关闭eginx
eginx -t	测试配置文件是否正确
eginx -v	打印版本号
eginx -V	打印版本号，编译器，配置参数等其他配置信息
ps aux | grep eginx	找到eginx所在路径
eginx -s stop	立即停止（不管不顾）
eginx -s quit	优雅停止（旧的进程收到命令，在此刻就停止链接，可能在此之前已经请求过来的，会继续提供服务直到服务完毕，没有新的内容需要处理了，再进行退出，线上推荐这种！！）
eginx -s reload	重启（收到重启命令后，检查新的配置文件的语法有效性，如果语法有问题不会重启。如果检查通过会启动新进程。直到旧的进程把它已经拥有的命令处理完毕后再退出旧的进程）
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















