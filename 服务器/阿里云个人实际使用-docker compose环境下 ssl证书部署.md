# ssl证书部署

## 背景

阿里云轻量服务器 *1

阿里云域名 *1

ICP本案已完成

公安备案进行中



服务器系统： 阿里云轻量应用服务器，2核2G4M，Ubuntu22.04

博客系统：halo

ssl部署方式：  docker compose,yaml文件配置。

证书使用阿里云免费的   DV-个人测试证书（免费版）证书。申请后，30分钟内审批通过，下载证书。



##  Docker Compose 配置nginx 挂载证书

### **步骤 1：项目目录结构**

首先，建议在服务器上创建一个清晰的目录结构来存放所有相关文件，这样便于管理。

  在项目的跟目录：

```plaintext
/halo项目根目录/
├── docker-compose.yml       # Docker Compose 的配置文件
├── nginx/
│   └── conf.d/
│       └── halo.conf  # Nginx 的站点配置文件
├── ssl/                     # 存放 SSL 证书的目录
│   ├── yourdomain.com.pem   # 证书文件   上面下载的证书压缩包两个中的一个文件
│   └── yourdomain.com.key   # 私钥文件    上面下载的证书压缩包两个中的一个文件
└── halo2/                     # halo2是自动生成的
    └── index.html
```

### **步骤 2：修改 `docker-compose.yml` 文件**

生成的 **`docker-compose.yml` 最终版本**（已集成 Halo、PostgreSQL、Nginx+SSL，直接粘贴即可用）：

```
services:
  # Halo博客服务
  halo:
    image: registry.fit2cloud.com/halo/halo:2.2.21
    container_name: halo
    depends_on:
      halodb:
        condition: service_healthy
    networks:
      - halo_network
    volumes:
      - ./halo2:/root/.halo2
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8090/actuator/health/readiness"]
      interval: 30s
      timeout: 5s
      retries: 3
    restart: on-failure:3
    environment:
      - JVM_OPTS=-Xmx256m -Xms256m
      - SPRING_R2DBC_URL=r2dbc:postgresql://halodb:5432/halo
      - SPRING_R2DBC_USERNAME=halo
      - SPRING_R2DBC_PASSWORD=openpostgresql
      - SPRING_SQL_INIT_PLATFORM=postgresql
      - HALO_EXTERNAL_URL=https://luyunxiao.xyz/  # 已替换为你的域名

  # PostgreSQL数据库服务
  halodb:
    image: postgres:15.4
    container_name: halodb
    networks:
      - halo_network
    volumes:
      - ./db:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD", "pg_isready"]
      interval: 10s
      timeout: 5s
      retries: 5
    restart: on-failure:3
    environment:
      - POSTGRES_PASSWORD=openpostgresql
      - POSTGRES_USER=halo
      - POSTGRES_DB=halo
      - POSTGRES_HOST_AUTH_METHOD=trust

  # Nginx+SSL服务（反向代理Halo）
  nginx:
    image: nginx:latest
    container_name: halo-nginx
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/conf.d:/etc/nginx/conf.d
      - ./ssl:/etc/nginx/ssl
    networks:
      - halo_network
    depends_on:
      - halo
    restart: always

# 自定义网络（让所有服务互通）
networks:
  halo_network:
```

### 配套 Nginx 配置（需放到 `./nginx/conf.d/halo.conf`）

```
# HTTP强制跳转HTTPS
server {
    listen 80;
    server_name luyunxiao.xyz www.luyunxiao.xyz;
    return 301 https://$host$request_uri;
}

# HTTPS配置（反向代理Halo）
server {
    listen 443 ssl;
    server_name luyunxiao.xyz www.luyunxiao.xyz;

    # SSL证书路径（对应./ssl目录下的文件）
    ssl_certificate /etc/nginx/ssl/luyunxiao.xyz.pem;
    ssl_certificate_key /etc/nginx/ssl/luyunxiao.xyz.key;

    # SSL优化配置
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384;
    ssl_prefer_server_ciphers on;

    # 反向代理到Halo
    location / {
        proxy_pass http://halo:8090;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## docker compose的重启

#### 1. 重启所有服务

这是最常用的命令，它会停止并重新创建所有正在运行的服务容器。

```bash
docker compose down && docker compose up -d
```

​     到这里就好了，如果报错，根据报错修改。

​    浏览器中通过域名访问自己的博客，小锁提示安全，则生效了。