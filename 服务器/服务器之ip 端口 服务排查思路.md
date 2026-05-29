# 排查流程

首先明确核心前提：`ping` 仅能排查**服务器 IP 连通性**（网络层），无法直接测端口 / 服务；排查端口需用 `telnet`/`nc`，服务是否正常要额外验证。以下是**结构化、可直接执行**的完整排查流程，覆盖 Linux/Ubuntu/CentOS/Windows 多环境，适配服务器运维场景。

## 前提准备

1. 确认目标信息：目标服务器公网 / 内网 IP（必填）、待排查端口（如 80/443/web、22/ssh、3306/mysql）、对应服务名称
2. 本地网络自检：先 ping 网关 / 百度（`ping 223.5.5.5`），确保本地网络无问题，避免误判
3. 工具准备：`ping` 全环境自带；`telnet` 部分环境需安装，下文附安装命令

------

## 第一步：ping 排查服务器 IP 连通性（网络层）

作用：验证本地 ↔ 目标服务器**网络是否通畅**，仅看 IP 可达性，和端口、服务无关

### 1. 执行命令（全环境通用）

```bash
# 基础命令（Windows/Linux通用），-c 4 表示发送4个包（Linux），Windows默认发不停，按Ctrl+C终止
ping 目标服务器IP       # 例：ping 192.168.1.100  /  ping 210.xxx.xxx.xxx
ping -c 4 目标服务器IP  # Linux专用，固定发包数，方便脚本执行
```

### 2. 结果解读（核心判断）

✅ 正常（IP 连通）：出现`来自xxx.xxx.xxx.xxx 的回复`（Windows）或`64 bytes from xxx`（Linux），丢包率 0%❌ 异常（IP 不通）：

1. `请求超时（Request timeout）`：大概率服务器防火墙禁 ping、服务器宕机、路由不通
2. `无法访问目标主机`：IP 错误、本地路由配置错误、公网 IP 未备案 / 未放行

### 3. 关键注意点

- 服务器为了安全，**大概率会禁 ping**（防火墙规则限制），此时 ping 不通≠服务器宕机，必须走下一步端口排查
- 仅公网 IP 需要考虑运营商 / 备案问题，内网 IP（如 192.168/172.16 段）优先查内网交换机 / 路由

------

## 第二步：telnet 排查端口是否开放（传输层）

作用：验证目标服务器**指定端口是否监听**，IP 通但端口不通，服务一定用不了；端口通，服务大概率正常（需进一步验证）

### 1. 先安装 telnet（部分环境缺失）

```bash
# 1. Linux（CentOS/RHEL）
yum install telnet -y

# 2. Linux（Ubuntu/Debian）
apt update && apt install telnet -y

# 3. Windows（启用telnet客户端）
控制面板 → 程序 → 启用或关闭Windows功能 → 勾选「Telnet客户端」→ 确定
```

### 2. 替代方案：nc（比 telnet 更稳定，推荐服务器用）

若 telnet 安装失败，用`nc`（netcat），Linux 优先装 nc：

```bash
# CentOS
yum install nc -y
# Ubuntu
apt install netcat -y

# nc 测端口命令（和telnet效果一致，更简洁）
nc -zv 目标IP 目标端口  # -z：仅扫描端口，-v：显示详细信息
```

### 3. 执行端口排查命令

```bash
# 核心命令（telnet通用）
telnet 目标服务器IP 目标端口  # 例：telnet 192.168.1.100 22  /  telnet 210.xxx.xxx.xxx 80

# 补充：Windows PowerShell 自带替代命令（无需装telnet）
Test-NetConnection 目标IP -Port 目标端口  # 例：Test-NetConnection 192.168.1.100 -Port 22
```

### 4. 结果解读（核心判断）

✅ 正常（端口开放）：

- telnet：进入黑屏界面（光标闪烁），或显示`Connected to xxx.xxx.xxx.xxx`

- nc：显示`xxx.xxx.xxx.xxx [目标IP] 目标端口 (tcp) open`

- PowerShell：显示

  ```
  TcpTestSucceeded : True
  ```

  ❌ 异常（端口未开放）：

1. `连接被拒绝（Connection refused）`：端口未监听（服务未启动）、端口配置错误
2. `连接超时（Connection timed out）`：端口被防火墙拦截（服务器防火墙 / 云安全组未放行）
3. `无法打开到主机的连接`：IP 不通（第一步已排查，此处可直接定位防火墙）

### 5. 关键注意点

- 云服务器（阿里云 / 腾讯云）需额外查**安全组**：必须放行目标端口，仅服务器防火墙放行没用
- 端口范围：1-65535，常用端口对应服务：22 (ssh)、80 (http)、443 (https)、3306 (mysql)、6379 (redis)

------

## 第三步：排查服务是否正常运行（应用层）

作用：端口开放≠服务正常（可能端口监听但服务进程异常），需验证服务本身可用性，分**通用排查**和**常见服务针对性排查**

### 1. 通用排查（登录服务器操作，核心）

先通过 ssh 登录服务器（若 22 端口通），排查服务进程 + 端口监听，适配 Linux 服务器（CentOS/Ubuntu 通用）

```bash
# 步骤1：查目标端口是否真的被进程监听（确认端口不是空监听）
netstat -tulpn | grep 目标端口  # -t：tcp，-u：udp，-l：监听，-p：进程，-n：数字格式
ss -tulpn | grep 目标端口       # 替代netstat，部分Linux默认无netstat，ss更高效

# 步骤2：查对应服务进程是否正常运行
systemctl status 服务名  # 系统服务（如nginx/ssh/mysql），例：systemctl status nginx
ps -ef | grep 服务名    # 所有进程，例：ps -ef | grep java（排查Java服务）

# 步骤3：服务异常修复（通用重启命令）
systemctl restart 服务名  # 例：systemctl restart nginx
```

### 2. 常见服务针对性排查（无需登录服务器，本地验证）

直接验证服务功能，更精准✅ Web 服务（80/443 端口，如 Nginx、Halo 博客）

- 本地浏览器访问：`http://目标IP`（80）/ `https://目标IP`（443），能打开页面 = 服务正常

- 命令行验证：

  ```
  curl 目标IP
  ```

  ，返回网页源码 = 正常

  ✅ SSH 服务（22 端口）

- 直接 ssh 登录：

  ```
  ssh 用户名@目标IP
  ```

  ，能输密码 = 服务正常

  

  ✅ 数据库服务（3306/mysql、6379/redis）

- mysql：`mysql -h 目标IP -u 用户名 -p`，能连接 = 正常

- redis：`redis-cli -h 目标IP -p 6379`，能进入交互界面 = 正常

------

## 完整排查逻辑（按顺序来，不跳步）

1. 先 ping IP → 通：走下一步；不通：先排查网络 / 防火墙禁 ping，再处理
2. 再 telnet/nc 端口 → 通：走下一步；不通：排查防火墙 / 安全组 / 服务未启动
3. 最后验证服务 → 正常：结束；异常：排查进程 / 配置 / 日志

------

## 常见问题快速定位（运维必备）

1. ping 通 + telnet 端口不通 → 90% 是**防火墙 / 安全组未放行端口**，10% 是服务未启动
2. telnet 端口通 + 服务用不了 → 服务进程异常（重启服务）、服务配置错误（查日志）
3. 内网通 + 公网不通 → 公网 IP 未备案、云安全组未放行公网、运营商拦截端口
4. 部分 IP 能通 + 部分 IP 不通 → 服务器做了 IP 白名单限制

```bash
# 基础命令（Windows/Linux通用），-c 4 表示发送4个包（Linux），Windows默认发不停，按Ctrl+C终止
ping 目标服务器IP       # 例：ping 192.168.1.100  /  ping 210.xxx.xxx.xxx
ping -c 4 目标服务器IP  # Linux专用，固定发包数，方便脚本执行
```