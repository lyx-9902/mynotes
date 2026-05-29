## 第一节：简介 Debian/Ubuntu 系统中nginx

Nginx 配置体系结构图（Debian/Ubuntu 版） **Debian/Ubuntu 专属设计**

 安装nginx后，系统中回自动生成如下的文件目录，该设计是linux下的经典设计。官方设计哲学。

顶层结构

```
/etc/nginx/
├── nginx.conf               # 全局总配置：进程、连接、日志、加载规则
│
├── conf.d/                  # 公共扩展配置（自动生效）
│   ├── gzip.conf
│   ├── ssl.conf
│   ├── cache.conf
│   └── *.conf               # 所有网站共用的规则
│
├── sites-available/         # 站点配置仓库（存放所有站点）
│   ├── site1.conf
│   ├── site2.conf
│   └── site3.conf
│
└── sites-enabled/           # 已启用站点（仅软链接） 禁止修改，只做命令行的删减操作。
    ├── site1.conf → ../sites-available/site1.conf
    └── site2.conf → ../sites-available/site2.conf
```

**自述解读：**

 安装nginx后， /etc/nginx/ 目录下，会有这几个关键文件，

**nginx.conf**   

**conf.d/**   该目录下放置自己的单系统配置。

**sites-available/**   站点配置仓库

**sites-enabled/**  该文件禁止修改（禁用指令删减)

  软连接的操作：见下列  **常用指令**

---



### 加载顺序（关键逻辑）

1. 先读：`nginx.conf`

2. 再自动包含：`conf.d/*.conf`

3. 最后包含：`sites-enabled/*`

   

nginx.conf 主配置里，包含指令。

```
    include /etc/nginx/conf.d/*.conf;   
    include /etc/nginx/sites-enabled/*;
```



### 职责一句话分清

- **nginx.conf**：定规矩，管全局
- **conf.d**：所有网站通用的配置片段
- **sites-available**：存所有站点的配置文件
- **sites-enabled**：只放链接，控制哪些站点**真正运行**

### 运维操作示意图

```
停用站点：删除 sites-enabled/ 链接
启用站点：ln -s 从 sites-available 链接过来
修改配置：只改 sites-available 里的原文件
```



### 浏览器请求 → Nginx 配置匹配流程图

```
用户在浏览器输入网址
       ↓
发起 HTTP/HTTPS 请求（带 Host、域名、端口）
       ↓
────────────────────────────────
到达 Nginx 服务器（监听 80 / 443 端口）
       ↓
【第一步：读全局配置】
/etc/nginx/nginx.conf
- 启动 worker 进程
- 加载全局规则
- 包含 conf.d/*.conf（通用规则）
- 包含 sites-enabled/*（站点配置）
       ↓
────────────────────────────────
【第二步：遍历所有 server 块】
Nginx 拿着请求里的：
  • 端口（listen）
  • 域名（server_name）
去匹配所有启用站点里的 server
       ↓
┌─────────────────────────────┐
│  匹配成功：进入对应 server   │
│  匹配失败：进入默认 server   │
└─────────────────────────────┘
       ↓
────────────────────────────────
【第三步：匹配 location 规则】
根据请求路径（/、/api、/static、/hls/xxx.flv 等）
按优先级匹配：

  精准 =      >  前缀 ^~    >  正则 ~ ~*   >  前缀 /
(location = )  (location ^~)  (location ~)   (location / )
       ↓
────────────────────────────────
【第四步：执行对应规则】
根据匹配到的 location 做处理：

  • root /var/www/html   → 直接返回静态文件
  • proxy_pass http://后端IP  → 转发请求（反向代理）
  • return 301 https://...  → 重定向
  • deny / allow        → 拦截或放行
  • fastcgi_pass        → 交给 PHP
       ↓
────────────────────────────────
【第五步：返回结果给用户】
Nginx 把响应发回浏览器
       ↓
页面加载 / 接口返回 / 视频播放
```

### 极简文字版（方便记）

1. 浏览器带**域名 + 路径**请求过来
2. Nginx 先加载**全局 + 所有启用站点**
3. 按**端口 + 域名**找到对应 `server`
4. 按**路径优先级**找到 `location`
5. 执行：**静态文件 / 反向代理 / 重定向 / 拒绝**
6. 返回结果



### 结合你之前的目录结构再对应一遍



```
/etc/nginx/nginx.conf        → 全局入口
conf.d/*.conf                → 通用规则（gzip、缓存、安全头）
sites-enabled/xxx.conf       → 真正参与匹配的 server + location
```





## 第二节：常用的指令：

### 操作软连接：

```
关联指令
ls -l /etc/nginx/sites-enabled/
```

ls = 列出文件
-l = 详细列表模式（显示权限、大小、链接、日期...）
/etc/nginx/sites-enabled/ = 要查看的目录
作用：查看当前 Nginx 启用了哪些网站。



1. 启用站点（只创建链接）bash运行

2. ln -s /etc/nginx/sites-available/你的站点.conf /etc/nginx/sites-enabled/
  → 只是创建快捷方式，没有修改任何配置内容。

3. 停用站点（只删除链接）bash运行

4. rm /etc/nginx/sites-enabled/你的站点.conf
  → 只是删掉快捷方式，原配置文件还在 sites-available 里，毫发无损。

  **重载配置**

```
nginx -t && systemctl reload nginx
```



### 端口占用根源确认

```
grep -r "listen" /etc/nginx/
```

grep = 搜索文本内容
-r = 递归搜索（进入所有子目录，一层层找）
"listen" = 要搜索的关键词
/etc/nginx/ = 在哪个目录里搜

输出结果代表什么？
你看到的结果大概是这样：

```
/etc/nginx/conf.d/myweb.conf: listen 8088;
/etc/nginx/sites-available/default: listen 80;
/etc/nginx/sites-available/default: listen [::]:80;
```

 帮你快速找到：到底哪个配置文件占用了 80 端口！





## 第三节： 部署docker - nginx 

```
Docker Nginx 目录结构（真实结构）plaintext/etc/nginx/
├── nginx.conf        # 主配置（只包含最基础配置）
└── conf.d/           # 只有这个目录！！！
    └── default.conf  # 唯一的站点配置（监听80端口
```

### 为什么 Docker Nginx 不用那两个目录？

因为 Docker 理念：

**一个容器 = 一个服务**

不需要多站点管理机制！

所以 Docker Nginx 只保留：

- `/etc/nginx/nginx.conf`
- `/etc/nginx/conf.d/*.conf`

**所有网站配置都直接丢进 conf.d/ 即可**

---



第一步：首先安装docker 

 第二步： 通过docker 拉取 nginx镜像



 容器创建项目案例：

```
sudo docker run -p 1029:80  -v /cetc/data/nginx/html:/usr/share/nginx/html -v /cetc/data/nginx/logs:/var/log/nginx -v /cetc/data/nginx/conf/nginx.conf:/etc/nginx/nginx.conf --restart=always --name nginx nginx:stable-alpine-perl
```



需要创建：
网页目录：/cetc/data/nginx/html     文件夹下：放置index.html文件

日志目录：/cetc/data/nginx/logs
配置文件：/cetc/data/nginx/conf/nginx.conf



### 一键创建所有目录 + 生成默认 nginx.conf



直接复制下面**整段命令**执行，一步到位：



```
# 创建目录
sudo mkdir -p /cetc/data/nginx/{html,logs,conf}

# 生成默认的 nginx.conf（必须有，否则容器启动失败）
sudo tee /cetc/data/nginx/conf/nginx.conf <<-'EOF'
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;

events {
    worker_connections  1024;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    keepalive_timeout  65;

    server {
        listen       80;
        server_name  localhost;

        root   /usr/share/nginx/html;
        index  index.html index.htm;

        location / {
            try_files $uri $uri/ =404;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
        }
    }
}
EOF

```



```
# 给权限（非常重要，否则容器无法读写）
sudo chmod -R 755 /cetc/data/nginx
sudo chown -R $USER:$USER /cetc/data/nginx
```

执行完后，**再运行你自己的 docker run 命令**就完全正常了。

### 访问方式

浏览器打开：

```
http://你的服务器IP:1029
```

