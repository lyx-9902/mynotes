# 本地养 OpenClaw

https://openclaw.ai/

https://docs.openclaw.ai/zh-CN

本地机器为win11 

安装OpenClaw

ai模型选择我公司内网的olama



## 打开「管理员权限」的 Windows 终端

按 `Win + X`

选择 **Windows 终端 (管理员)**

一定要管理员，不然权限不够。

安装 Node.js（OpenClaw 需要）

```
node -v
npm -v


v22.12.0
10.9.0
```

 安装 OpenClaw

```
npm install -g openclaw --registry=https://registry.npmmirror.com
```

验证：

```
openclaw --version

2026.3.2
```



\# 测试 Ollama 连通性 Invoke-RestMethod -Uri "http://192.168.112.3:11434/api/tags" -Method Get







###  最推荐：使用专用命令 (CLI)

这是最标准、最直接的方法，所有操作在命令行里一键完成。

| 操作         | 命令 (在PowerShell或CMD中运行)                 | 说明                                           |
| :----------- | :--------------------------------------------- | :--------------------------------------------- |
| **启动**     | `openclaw gateway start`                       | 在后台启动OpenClaw的核心服务。                 |
| **关闭**     | `openclaw gateway stop`                        | 优雅地停止后台服务，释放系统资源。             |
| **重启**     | `openclaw gateway restart`                     | 当你修改了配置文件后，执行此命令让新配置生效。 |
| **查看状态** | `openclaw gateway status` 或 `openclaw status` | 确认服务当前是在运行还是停止状态。             |





## 阿里云轻量服务器 ubuntu  连接飞书。

查看linux系统信息 

```
cat /etc/os-release

PRETTY_NAME="Ubuntu 24.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.3 LTS (Noble Numbat)"

```



 准备环境

安装nodejs 

```
# 安装 Node.js
sudo apt install -y nodejs

# 验证版本（确保 ≥22.x）
node --version
npm --version
```



结果： 2核2g 内存过小，卡死。







# Linux子系统安装

 win电脑上，子系统WSL安装，





external-controller: 0.0.0.0:9097





安装WSL

 ubuntu:    lyx 123456



 进入方法：  打开powell shell  输入 wsl  



```
快速安装
curl -fsSL https://openclaw.ai/install.sh | bash
```



```
WSL 里有几个发行版：
 指令：
wsl -d Ubuntu

进入指定ubuntu的环境中去
wsl -d Ubuntu
```



**Docker Desktop 自带的 WSL 环境** 里

直接输入 `exit` 并回车



虚拟环境如果有多个，指令 wsl，会进入默认的一个。需要注意。







哔哩哔教程

https://www.bilibili.com/video/BV1rHNuzoEsb/?spm_id_from=333.337.search-card.all.click&vd_source=08704ab849ba956e9d7acbdbd55b0991







停止服务

openclaw gateway stop







2026.05.29  今天卸载了龙虾。 原因： 没有感受到龙虾的便利。

