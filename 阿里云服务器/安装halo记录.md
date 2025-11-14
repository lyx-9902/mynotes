# 使用docker compose部署博客项目

## 一 、服务器配置

判断服务器类别

```
指令： cat /etc/os-release

PRETTY_NAME="Ubuntu 24.04.2 LTS"
NAME="Ubuntu"
```

## 二、部署思路

Ubuntu服务器上，部署 docker compose启动服务，原因是部署方面，环境隔离。

## 三、具体操作

### 安装 docker  docker compose

#### 1. 快速更新系统（可选，加速后续安装）

 首先更新软件索引

```
sudo apt update -y
  这条命令在基于 Debian 的 Linux 系统（如 Ubuntu）中用于更新和升级软件包，确保系统保持最新状态并修复已知漏洞。
```

**apt**（Advanced Packaging Tool）是Debian和Ubuntu等基于Debian的Linux发行版中使用的软件包管理器。它提供了一种简洁的命令行界面来执行软件包的安装、更新、升级和删除等操作。使用apt命令通常需要超级用户权限

**sudo**: **sudo** 命令允许普通用户以超级用户（root）的身份执行命令。它是 Linux 系统中非常重要的命令，尤其在需要执行系统管理任务时。

#### 2. 一键安装 Docker 核心组件

```
apt install docker.io

apt install docker-compose-plugin
```

>  备注： 安装docker过程中，大概率碰到镜像地址无法访问的问题，需要梯子才能拉取镜像。 另一个方法就是更换为国内镜像。见文末。



### 3.按照文档安装

[使用 Docker Compose 部署](https://docs.halo.run/getting-started/install/docker-compose)

Halo + PostgresQL(推荐)，按照推荐方式安装了。

 但是，浏览器无法访问    (⊙︿⊙)  

#### 4.防火墙

查看 yaml配置中是  ports:      - "8090:8090"。

具体操作是，登录阿里云控制台，进入服务器》防火墙, 默认开发80， 443，添加一条8090规则。

添加成功后，稍等2-3分钟后，刷新页面，可以了。接下来进入配置博客。







#### linux系统更换国内镜像

编辑 sources.list 文件

使用文本编辑器打开 */etc/apt/sources.list* 文件：

```
sudo nano /etc/apt/sources.list
```

将文件中的内容替换为新的镜像源地址。例如，使用阿里云镜像源

```
deb http://mirrors.aliyun.com/ubuntu/ <版本代号> main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ <版本代号>-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ <版本代号>-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ <版本代号>-backports main restricted universe multiverse
```

将 *<版本代号>* 替换为实际的系统版本代号（如 *focal* 或 *jammy*）。

你的服务器是 **Ubuntu 24.04.2 LTS**，对应的版本代号是 **`noble`**（Ubuntu 版本代号固定，24.04 官方代号为 `noble`，全称为 `Noble Numbat`）。

以下是替换后的 **阿里云 Ubuntu 源配置**（可直接复制使用）：

```
deb http://mirrors.aliyun.com/ubuntu/ noble main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ noble-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ noble-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ noble-backports main restricted universe multiverse
```

保存并退出编辑器后，运行以下命令更新软件包列表：

```
sudo apt update && sudo apt upgrade -y
```

可以安装想要的软件了



**退出编辑方式：**

如果你是在 **Linux 终端的文本编辑器**（如 `nano` 或 `vi/vim`）中想要退出编辑状态，操作如下：

情况 1：使用 `nano` 编辑器

- 按 `Ctrl + X` → 若有修改，会询问是否保存，按 `Y` 保存、`N` 不保存，再按回车键确认即可退出。

情况 2：使用 `vi/vim` 编辑器

- 先按 `Esc` 键确保进入**普通模式** → 然后输入 `:q`（不保存退出）或 `:wq`（保存并退出），最后按回车键执行。



文末： 部署完，查看FinalShell，启动这些就占用了33G，占用太大了。后面想办法改进吧。谁有好办法，也可以 留言我，感谢。

