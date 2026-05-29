### 一、环境准备

1. 更新系统包

   （确保依赖最新）：

   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. 检查 Ubuntu 版本

   （兼容 18.04/20.04/22.04 等主流版本）：

   ```bash
   lsb_release -a
   ```

### 二、安装 Nginx

#### 方式 1：官方源安装（推荐，版本最新）

1. 安装依赖：

   ```bash
   sudo apt install -y curl gnupg2 ca-certificates lsb-release ubuntu-keyring
   ```

2. 添加 Nginx 官方 GPG 密钥：

   ```bash
   curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null
   ```

3. 添加 Nginx 源（以稳定版为例）：

   ```bash
   echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] http://nginx.org/packages/ubuntu $(lsb_release -cs) nginx" | sudo tee /etc/apt/sources.list.d/nginx.list
   ```

4. 安装 Nginx：

   ```bash
   sudo apt update && sudo apt install -y nginx
   ```



```bash
apt install -y nginx
```

1.启动 Nginx 服务：

```
sudo systemctl start nginx
```

2.设置开机自启：

```
sudo systemctl enable nginx
```

3.检查服务状态（显示 `active (running)` 则正常）：

```
sudo systemctl status nginx
```



## 其他命令：

**强制重启 Nginx（让新配置生效）**：

```
sudo systemctl restart nginx

sudo nginx -s reload
```

**验证最终监听端口**：

重启后执行：

```
sudo ss -tulpn | grep nginx
```

#### 验证配置（确认 80 端口监听已移除）

```
sudo nginx -T | grep -E "listen 80"
```

- 若无输出，说明 80 端口监听已清理；
- 若仍有输出，检查 `/etc/nginx/conf.d/` 目录下是否有其他包含 `listen 80` 的文件（Ubuntu 部分版本会在 `conf.d/default.conf` 也放默认配置）。

### 在 Ubuntu 中停止 Nginx 服务

```
sudo systemctl stop nginx
```





## 检查是否已经安装了nginx

nginx -v  # 仅显示版本号
# 或
nginx -V  # 显示版本 + 编译参数（更详细）

如何提示not found则是没有安装。



docker compose restart halo     用于重启容器 例如修改了配置文件

docker compose down halo 停止容器  （docker compose down 是停止yml中所有的服务）

docker compose up -d halo 启动容器

# 进入web容器 shell环境（替换为你的容器名/服务名）

docker compose exec <web服务名> sh
退出shell： 输入exit   然后 enter键 

进入容器命令行后
  退出：  ctrl + p 

安装nginx
netstat -tulpn | grep -E ":80|:443"     # 看是否被其他程序占用



```
nginx -v   打印版本号  也可以检查是否安装
```





### 关于在ubuntu中，nginx镜像一直无法使用的解决办法之一

使用一个能正常拉取镜像的机器，拉取后，下载到本地。然后再拖进不能连接镜像发的机器，按照nginx包使用方法。

