# docker使用记录

##  0.使用过程中，碰到的小问题

dos 命令：  

windows系统下使用cd命令切换到D盘的方法： 

解决方法

方法一：使用下面这条命令

```
cd /d d:
```

方法二：直接使用

```
d:
```

https://blog.csdn.net/ZNJIAYOUYA/article/details/123169561



 关于docker的镜像问题：  官方的镜像可以网络问题，无法使用， 例如：初始化项目拉去eginx镜像的时候，报错。

  处理方法：

**Windows（Docker For Windows）**

Windows系统上的Docker For Windows用户可以按照以下步骤配置镜像加速服务：

1. 在桌面右下角状态栏中右键docker图标，修改在Docker Daemon标签页中的json。
2. 将以下地址加入"registry-mirrors"的数组里。[`https://docker.xuanyuan.me`](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdocker.xuanyuan.me%2F&objectId=2485043&objectType=1&contentType=undefined)
3. 点击Apply，重新生成Docker环境以使配置生效。



 国内镜像网站： https://docker.xuanyuan.me/   轩辕镜像





## 1.docker指令：

**docker ps**

```
docker ps 命令用于列出 Docker 容器。

默认情况下，docker ps 命令只显示运行中的容器，但也可以通过指定选项来显示所有容器，包括停止的容器。

语法
docker ps [OPTIONS]
OPTIONS说明：

-a, --all: 显示所有容器，包括停止的容器。
-q, --quiet: 只显示容器 ID。
-l, --latest: 显示最近创建的一个容器，包括所有状态。
-n: 显示最近创建的 n 个容器，包括所有状态。
--no-trunc: 不截断输出。
-s, --size: 显示容器的大小。
--filter, -f: 根据条件过滤显示的容器。
--format: 格式化输出。

```

docker ps

PS F:\nginx-web> docker ps
CONTAINER ID   IMAGE          COMMAND                   CREATED       STATUS       PORTS                  NAMES
6e89dc2f54dc   nginx:latest   "/docker-entrypoint.…"   2 hours ago   Up 2 hours   0.0.0.0:8080->80/tcp   nginx-test

输出详情介绍：

**CONTAINER ID:** 容器 ID。

**IMAGE:** 使用的镜像。

**COMMAND:** 启动容器时运行的命令。

**CREATED:** 容器的创建时间。

**STATUS:** 容器状态。

状态有7种：

- created（已创建）
- restarting（重启中）
- running（运行中）
- removing（迁移中）
- paused（暂停）
- exited（停止）
- dead（死亡）

**PORTS:** 容器的端口信息和使用的连接类型（tcp\udp）。 （上面示例： 外部访问8080 -- 映射容器中的80端口）

**NAMES:** 自动分配的容器名称。

**2、列出所有容器，包括停止的容器**

```
docker ps -a
```

显示所有容器，包括停止的容器。

**3、只显示容器 ID**

```
docker ps -q
```

只显示容器 ID。

**4、显示最近创建的一个容器**

```
docker ps -l
```

显示最近创建的一个容器，包括所有状态。

**5、显示最近创建的 n 个容器**

```
docker ps -n 3
```

显示最近创建的 3 个容器，包括所有状态。

**6、显示容器的大小**

```
docker ps -s
```

显示容器的大小。

**7、根据条件过滤显示的容器**

```
docker ps -f "status=exited"
```

显示状态为 exited 的容器。

```
docker ps -f "name=my_container"
```

显示名称包含 my_container 的容器。

**8、格式化输出**

```
docker ps --format "table {{.ID}}\t{{.Names}}\t{{.Status}}"
```

以表格形式显示容器的 ID、名称和状态。

**常见过滤器**

- **`status`**: 容器状态（如 `running`、`paused`、`exited`）。
- **`name`**: 容器名称。
- **`id`**: 容器 ID。
- **`label`**: 容器标签。
- **`ancestor`**: 容器镜像。

**使用场景**

- **监控容器状态**: 实时监控运行中的容器状态和资源使用情况。
- **调试和管理**: 查看所有容器，包括停止的容器，以便进行调试和管理操作。
- **自动化脚本**: 使用过滤器和格式化选项，便于在自动化脚本中获取特定容器信息。



   **操作顺序：** 

第一步： 

 **docker ps**  

​      查看容器中有哪些保活的容器。 记住容器id

第二步：

​     停止一个正在运行的容器 

 1.优雅的停止 

  **docker stop 6e89dc2f54dc**   

> docker stop 容器ID或容器名
> 参数 -t：关闭容器的限时，如果超时未能关闭则用kill强制关闭，默认值10s，这个时间用于容器的自己保存状态
> docker stop -t=60 容器ID或容器名

2.docker kill

> docker kill 容器ID或容器名 :直接关闭容器

​     由此可见stop和kill的主要区别:stop给与一定的关闭时间交由容器自己保存状态，kill直接关闭容器

三、重启一个容器

docker restart 容器ID或容器名 ：不管容器是否启动，直接重启容器
1. 首先 docker ps 查看正在运行的容器信息，显示2分钟前启动运行
2. docker restart 59ec   重启容器
3. 再次 docker ps 查看容器信息 显示 2秒前启动运行
    ————————————————
    版权声明：本文为CSDN博主「Michel4Liu」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
    原文链接：https://blog.csdn.net/Michel4Liu/article/details/80889977



## 指令表格总结：

| 操作需求               | 命令                                                         |
| ---------------------- | ------------------------------------------------------------ |
| 查看运行中的容器       | `docker ps`                                                  |
| 查看所有容器（含停止） | `docker ps -a`                                               |
| 停止容器               | `docker stop 容器名称/容器ID`（如 `docker stop node-site-container`） |
| 启动已停止的容器       | `docker start 容器名称/容器ID`                               |
| 删除容器（需先停止）   | `docker rm 容器名称/容器ID`                                  |
| 删除镜像               | `docker rmi 镜像名称:版本`（如 `docker rmi my-node-site:v1`） |
| 实时查看容器日志       | `docker logs -f 容器名称`                                    |



## 2.案例：docker中使用nginx镜像 启动一个web服务

在 Windows 11 的 Docker Desktop 中用 Nginx 启动 Web 服务，核心是 **“基于官方 Nginx 镜像，通过文件挂载 / 自定义镜像两种方式”** 部署（推荐文件挂载，无需重复构建镜像，修改网站文件实时生效）。以下是最简洁、可落地的完整步骤：

**一、核心思路**

Nginx 是高性能 Web 服务器，Docker 中直接使用官方 `nginx` 镜像，通过 **端口映射**（让本地能访问容器内 Nginx）和 **目录挂载**（本地网站文件直接同步到容器，无需重新构建镜像）快速启动服务。

**二、详细步骤（推荐「文件挂载」方式）**

1. 准备本地网站文件和 Nginx 配置（关键）

先在本地创建文件夹，用于存放网站文件和 Nginx 配置（方便后续修改）：

- 新建根目录：`C:\Docker\nginx-web`（可自定义路径，避免中文 / 空格）

- 在根目录下创建 2 个子文件夹：

  ```plaintext
  nginx-web/
  ├── html/          # 存放你的网站文件（HTML/CSS/JS）
  └── conf/          # 存放自定义 Nginx 配置（可选，默认用官方配置也能运行）
  ```

**（1）准备网站文件**

在 `html` 文件夹中新建 `index.html`（测试用，可替换为你的实际网站文件）：

html

```html
<!DOCTYPE html>
<html>
<head>
    <title>Docker Nginx Web 服务</title>
    <meta charset="utf-8">
    <style>
        body { text-align: center; margin-top: 100px; font-size: 24px; }
    </style>
</head>
<body>
    <h1>✅ Docker + Nginx 服务启动成功！</h1>
    <p>Windows 11 Docker Desktop 部署</p>
</body>
</html>
```

**（2）自定义 Nginx 配置（可选，推荐）**

如果需要修改 Nginx 端口、根目录、反向代理等，在 `conf` 文件夹中新建 `nginx.conf`（默认配置可直接用，以下是简化版）：

nginx

```nginx
#  worker 进程数（默认自动适配 CPU 核心）
worker_processes  1;

events {
    worker_connections  1024;  # 每个 worker 最大连接数
}

http {
    include       mime.types;  # 支持的文件类型
    default_type  application/octet-stream;

    # 日志格式（可选，默认开启）
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;  # 访问日志路径（容器内）

    sendfile        on;  # 开启高效文件传输
    keepalive_timeout  65;  # 长连接超时时间

    # 虚拟主机配置（核心）
    server {
        listen       80;  # Nginx 容器内端口（必须和后续端口映射对应）
        server_name  localhost;  # 域名（本地访问用 localhost）

        # 网站根目录（容器内路径，需和挂载的本地目录对应）
        root   /usr/share/nginx/html;
        index  index.html index.htm;  # 默认首页

        # 404 页面配置（可选）
        error_page  404              /404.html;
        location = /404.html {
            root   /usr/share/nginx/html;
        }

        # 50x 错误页面配置（可选）
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /usr/share/nginx/html;
        }
    }
}
```

**2. 拉取官方 Nginx 镜像**

打开 **Windows 终端（管理员模式）** 或 CMD，执行命令拉取最新版 Nginx 镜像：

bash

```bash
docker pull nginx:latest
```

- 拉取成功后，执行 `docker images` 可看到 `nginx` 镜像（TAG 为 `latest`）。

**3. 启动 Nginx 容器（关键：端口映射 + 目录挂载）**

执行以下命令，启动容器并关联本地文件（复制粘贴到终端即可，注意路径替换）：



```bash
输入启动指令，按如下执行
docker run -d -p 8080:80 --name nginx-test nginx:latest

docker run -d -p 8080:88 -v F:\nginx-web\html:/usr/share/nginx/html -v F:\nginx-web\conf\nginx.conf:/etc/nginx/nginx.conf --name nginx-test nginx:latest

指令解释：
docker run -d \
  --name nginx-web-server \  # 容器名称（自定义，方便后续操作）
  -p 8080:80 \               # 端口映射：本地 8080 端口 → 容器 80 端口（Nginx 默认端口）
  -v C:\Docker\nginx-web\html:/usr/share/nginx/html \  # 挂载网站文件：本地 html 文件夹 → 容器 Nginx 根目录
  -v C:\Docker\nginx-web\conf\nginx.conf:/etc/nginx/nginx.conf \  # 挂载配置文件：本地 conf → 容器 Nginx 配置
  --restart always \         # 可选：Docker 重启时自动启动容器
  nginx:latest

```

  

 本案例： 是在F：盘下，新建了一个文件夹为 nginx-web，

```
nginx-web
  |---- conf -- nginx.conf 配置文件
  |---- html- 一个index.html文件
```



docker run -d -p 8080:80 -v F:\nginx-web\html:/usr/share/nginx/html -v F:\nginx-web\conf\nginx.conf:/etc/nginx/nginx.conf --name nginx-test nginx:latest

解释：

 使用docker 跑一个容器。

 端口映射为 外8080--对应容器中的80端口  

F:\nginx-web\html   映射容器中的  /usr/share/nginx/html

F:\nginx-web\conf\nginx.conf  映射容器中的/etc/nginx/nginx.conf

容器名字是： nginx-test

nginx:latest  拉去最新的镜像 

​           dos命令 执行后， 浏览器可以输入查看网页  http://127.0.0.1:8080/

​           效果：更改nginx-web中的 html项目内容，只要保存一下，浏览器中刷新，即可。不需要重新启动docker。

​                         nginx.conf 配置文件，修改后，不需要重新启动docker.

>  下面可以看到： nginx监听的80端口，就是容器内的端口。 这个端口，外部是无法访问的，通过创建容器的时候，暴漏一个外部端口8080，来访问

```nginx
#  worker 进程数（默认自动适配 CPU 核心）
worker_processes  1;

events {
    worker_connections  1024;  # 每个 worker 最大连接数
}

http {
    include       mime.types;  # 支持的文件类型
    default_type  application/octet-stream;

    # 日志格式（可选，默认开启）
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;  # 访问日志路径（容器内）

    sendfile        on;  # 开启高效文件传输
    keepalive_timeout  65;  # 长连接超时时间

    # 虚拟主机配置（核心）
    server {
        listen       80;  # Nginx 容器内端口（必须和后续端口映射对应）
        server_name  localhost;  # 域名（本地访问用 localhost）

        # 网站根目录（容器内路径，需和挂载的本地目录对应）
        root   /usr/share/nginx/html;
        index  index.html index.htm;  # 默认首页

        # 404 页面配置（可选）
        error_page  404              /404.html;
        location = /404.html {
            root   /usr/share/nginx/html;
        }

        # 50x 错误页面配置（可选）
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /usr/share/nginx/html;
        }
    }
}
```

总结： 本地测试，如果更新了容器内的80端口为88，需要将容器重新启动，修改监听端口。





## 3.容器内的web可以访问外网的资源吗

在 Docker 容器中，Web 服务**默认是可以访问外网资源的**，因为 Docker 容器与宿主机共享网络栈（除非手动配置了网络隔离）。以下是具体说明和验证方法：

### 一、默认行为：容器可直接访问外网

Docker 容器在启动时，默认使用 `bridge` 网络模式，该模式下容器会通过宿主机的网络连接访问外网。例如，容器内的 Web 服务可以：

- 加载外部 CDN 资源（如 `https://cdn.jsdelivr.net/npm/vue@3`）；
- 调用第三方 API（如天气接口、支付接口等）；
- 下载依赖（如 Node.js 容器中 `npm install` 会从外网拉取包）。

### 二、验证方法：进入容器测试外网访问

以 Nginx 容器为例，执行以下步骤验证：

1. **进入容器终端**：

   bash

   ```bash
   docker exec -it 你的容器名称 /bin/bash
   
    docker exec -it nginx-test /bin/bash     注意点：nginx-test 一个空格/bin/bash  说明这是两个参数
   ```

2. **测试访问外网**：

   ```bash
   curl https://www.baidu.com
   ```

   若返回百度的 HTML 内容，说明容器可正常访问外网。

3.退出容器终端：

​                           方式 1：优雅退出（推荐，不终止容器）

在容器终端中，直接输入以下命令并回车：

bash

```bash
exit
```

执行后会立即返回宿主机（Windows 11）的终端界面，容器保持后台运行（可通过 `docker ps` 验证容器仍在运行）。

​                          方式 2：快捷键强制退出（快速，同样不终止容器）

如果觉得输入 `exit` 麻烦，直接按键盘快捷键：

```plaintext
Ctrl + P + Q
```

- 按顺序快速按下 `Ctrl`+`P`，再松开按 `Q`（无需输入任何命令）；
- 瞬间返回宿主机终端，容器继续运行，适合快速切换场景。



### 三、特殊情况：无法访问外网的原因及解决

如果容器确实无法访问外网，可能是以下原因：

| 原因                    | 解决方法                                                     |
| ----------------------- | ------------------------------------------------------------ |
| **宿主机本身无外网**    | 检查宿主机是否能正常上网（如浏览器打开百度），解决宿主机网络问题后重试。 |
| **Docker 网络配置异常** | 重置 Docker 网络：`docker network prune`（删除所有未使用的网络）重启 Docker 后重新启动容器。 |
| **防火墙拦截**          | 检查宿主机防火墙是否放行 Docker 相关流量（Windows 可临时关闭防火墙测试，Linux 可执行 `ufw allow 2375` 等）。 |
| **自定义网络模式**      | 若手动配置了 `none` 或 `host` 以外的自定义网络，需确保该网络的网关和 DNS 配置正确。 |

### 四、实战示例：Web 服务加载外网资源

假设你的 Web 页面需要加载外部 Vue 资源，代码如下：

```html
<!DOCTYPE html>
<html>
<head>
  <title>访问外网资源测试</title>
  <!-- 加载外部 CDN 资源 -->
  <script src="https://cdn.jsdelivr.net/npm/vue@3"></script>
</head>
<body>
  <div id="app">{{ message }}</div>
  <script>
    const app = Vue.createApp({
      data() {
        return { message: "成功加载外网 Vue 资源！" };
      }
    });
    app.mount('#app');
  </script>
</body>
</html>
```

将该文件放入 Nginx 挂载的 `html` 目录后，访问 `http://localhost:8080`，若页面正常显示 “成功加载外网 Vue 资源！”，则证明容器内 Web 服务可正常访问外网资源。

综上，**Docker 容器内的 Web 服务默认支持访问外网资源**，若出现异常可通过上述方法排查解决。



####  总结：

**第一个**：*sudo docker exec -it 容器id /bin/bash* 是一个常用命令，用于进入正在运行的 Docker 容器并启动一个交互式的 Bash Shell。

```
docker exec -it 你的容器名称 /bin/bash
```

**第二个**：curl 是常用的命令行工具，用来请求 Web 服务器。

```bash
curl https://www.baidu.com
```

上面命令向`www.example.com`发出 GET 请求，服务器返回的内容会在命令行输出。

[curl 的用法指南](https://www.ruanyifeng.com/blog/2019/09/curl-reference.html)



## 易错点： docker compose 和cocker-compose区别

在 Docker 生态中，`docker compose`（**内置插件**）和 `docker-compose`（**独立工具**）是两个核心但易混淆的组件，核心区别在于**安装方式、版本归属、功能支持**，版本区分和使用注意事项直接影响项目兼容性，下面分点详细说明：

## 一、核心区别：`docker compose` vs `docker-compose`

| 对比维度     | `docker compose`（内置插件）                                 | `docker-compose`（独立工具）                                 |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **本质**     | Docker 官方内置的 **命令行插件**（随 Docker 安装）           | Python 开发的 **独立第三方工具**（需单独安装）               |
| **安装方式** | 1. Docker Desktop（Windows/Mac）默认集成；2. Linux 需通过 Docker 官方仓库安装（`docker compose` 是 `docker-ce-cli` 的子组件） | 1. `pip install docker-compose`（Python 依赖）；2. 下载官方二进制文件；3. 系统包管理器（如 `apt install docker-compose`，版本可能老旧） |
| **命令格式** | 无连字符：`docker compose up`、`docker compose down`         | 有连字符：`docker-compose up`、`docker-compose down`         |
| **版本归属** | 版本号与 Docker 引擎对齐（如 Docker 20.10+ 对应 compose 插件 v2+） | 独立版本号（如 1.29.2、1.28.5，最新稳定版为 1.29.2）         |
| **核心依赖** | 基于 Go 语言开发，依赖 Docker 引擎（无需 Python）            | 基于 Python 开发，依赖 `docker-py` 库（Python 2/3）          |
| **功能支持** | 支持 Compose Specification 最新特性（如 `profiles`、`extends` 增强、`secrets` 原生支持） | 仅支持 Compose v3 及部分旧特性，不支持最新 Specification（如 `profiles` 是后期兼容，部分功能缺失） |
| **兼容性**   | 向下兼容大部分 `docker-compose.yml`（v2/v3 格式），但部分旧语法可能警告 | 兼容 v1/v2/v3 格式，但不支持新特性（如 `services.*.deploy.replicas` 在 Swarm 外无效） |
| **维护状态** | 官方主推，持续更新（活跃维护）                               | 已进入 **维护模式**（仅修复关键 Bug，不再新增功能）          |
| **适用场景** | 新项目、需要使用最新特性、追求稳定性和官方支持               | 旧项目迁移、依赖特定旧版本功能、临时测试                     |



## 总结

| 工具 / 概念      | 关键结论                                          |
| ---------------- | ------------------------------------------------- |
| `docker compose` | 官方主推、无连字符、Go 开发、支持最新特性         |
| `docker-compose` | legacy 工具、有连字符、Python 开发、仅维护        |
| Compose 文件格式 | 新项目省略 `version:`，用 Compose Specification   |
| 优先级           | `docker compose`（v2+） > `docker-compose`（1.x） |





