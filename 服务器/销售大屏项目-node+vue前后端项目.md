# PM2 完整简介

## 一、什么是 PM2

PM2 是一款**基于 Node.js 的生产环境进程管理工具**，全称 Process Manager 2，专门用来托管 Node 后端服务（Express/Koa/Nest/Egg 等），解决 Node 单进程崩溃、开机自启、日志、负载均衡、监控等运维问题。

## 二、核心作用

1. 进程守护（保活）

   

   Node 默认单进程，代码报错、内存溢出、异常退出会直接挂服务；PM2 自动检测进程崩溃，

   立即重启

   ，保障线上服务不间断。

2. 集群负载均衡 Cluster Mode

   

   利用多核 CPU，自动创建多实例平分请求，充分利用服务器性能，提升并发承载。

3. 日志统一管理

   

   自动拆分标准输出日志、错误日志，支持日志切割、持久化存储，不用自己写文件逻辑。

4. 服务开机自启

   

   服务器断电重启后，一键配置系统服务（systemd/windows 服务），自动拉起所有托管项目。

5. 实时监控面板

   

   查看 CPU、内存占用、进程状态、重启次数、运行时长，自带命令行监控与 Web 可视化监控。

6. 平滑重启 / 热重载

   - `pm2 reload`：零停机更新代码，旧进程处理完现有请求再销毁，无业务中断；
   - `pm2 restart`：强制重启；
   - `pm2 gracefulReload` 优雅关闭。

7. 环境隔离

   

   支持在配置文件中区分开发、测试、生产环境变量。

8. 远程部署、版本回滚

   

   配套 pm2 deploy 实现服务器一键发布、回滚版本。

## 三、适用场景

- Node.js 后端接口服务（Express、Koa、NestJS）
- 定时脚本、消息消费队列、爬虫常驻脚本
- 需要 7×24 小时稳定运行的长驻 Node 程序

## 四、基础特性对比原生 node 运行

|    方式     | 崩溃自动重启 | 多核集群 | 日志持久化 | 开机自启 | 监控 | 零停机更新 |
| :---------: | :----------: | :------: | :--------: | :------: | :--: | :--------: |
| node app.js |      ❌       |    ❌     |     ❌      |    ❌     |  ❌   |     ❌      |
|     PM2     |      ✅       |    ✅     |     ✅      |    ✅     |  ✅   |     ✅      |

## 五、安装与极简使用

### 1. 全局安装

```
npm install pm2 -g
```

### 2. 常用基础命令

bash

```
# 启动项目，命名为 api
pm2 start app.js --name api

# 集群模式启动，使用全部CPU核心
pm2 start app.js -i max

# 查看所有进程列表
pm2 list

# 实时监控
pm2 monit

# 平滑重启（不中断请求）
pm2 reload api

# 强制重启
pm2 restart api

# 停止/删除进程
pm2 stop api
pm2 delete api

# 保存当前进程列表，设置开机自启
pm2 save
pm2 startup
```

## 六、配置文件 ecosystem.config.js

企业级项目统一配置，无需长命令：

js

```
module.exports = {
  apps: [{
    name: "server",
    script: "./dist/main.js",
    instances: "max", // 多核集群
    exec_mode: "cluster",
    env: { NODE_ENV: "development" },
    env_production: { NODE_ENV: "production" },
    out_file: "./logs/out.log", // 正常日志
    error_file: "./logs/err.log", // 错误日志
    max_memory_restart: "300M" // 内存超过300M自动重启
  }]
}
```

启动：`pm2 start ecosystem.config.js --env production`

## 七、优缺点

### 优点

1. 零侵入，不用修改业务代码；
2. 运维能力齐全，中小型 Node 服务标配；
3. 跨平台：Linux / MacOS / Windows 全支持；
4. 轻量，性能损耗极低。

### 局限

1. 仅原生适配 Node.js，不适合 Java/Python/Go 等其他语言程序；
2. 单机进程管理，分布式多机器集群场景建议搭配 K8s。

## 八、定位总结

PM2 是**单机 Node 应用最佳进程管理器**，是线上部署 Node 服务的标准工具，负责进程保活、性能调度、运维监控，替代手动 `nohup node app &` 简陋后台运行方案。

# dotenv 简介

# dotenv 完整简介

## 一、什么是 dotenv

`dotenv` 是 Node.js 生态最常用的**环境变量管理库**，作用是读取项目根目录下 `.env` 文件中的自定义环境变量，并注入到 `process.env` 全局对象，实现配置与代码分离。

### 核心解决痛点

1. 敏感配置（数据库账号、密钥、端口、第三方 token）硬编码写在代码里，容易泄露；
2. 开发 / 测试 / 生产环境配置不一致，切换麻烦；
3. 避免把账号密码提交到 Git 仓库。

## 二、工作原理

1. 项目新建 `.env` 文件，以 `KEY=VALUE` 格式写配置；
2. 程序启动时加载 dotenv，自动解析 `.env`；
3. 将所有键值挂载到 Node 全局 `process.env`，代码直接读取使用。

## 三、基础使用

### 1. 安装

bash



运行







```
npm install dotenv
# 或 yarn add dotenv
```

### 2. 创建 .env 文件（项目根目录）

env









```
# .env
# 服务端口
PORT=3000
# 数据库配置
DB_HOST=127.0.0.1
DB_USER=root
DB_PASS=123456
# 密钥
JWT_SECRET=abc123secret
```

### 3. 入口文件加载（必须放在最顶部）

js



运行







```
// app.js / main.js
require('dotenv').config()

// 读取环境变量
console.log(process.env.PORT)
console.log(process.env.DB_USER)
```

### ES Module 写法

js



运行







```
import 'dotenv/config'
```

## 四、多环境区分（开发 / 生产）

dotenv 支持多份 env 文件区分环境，搭配 `dotenv-expand` 可支持变量嵌套：

- `.env` 通用默认配置
- `.env.development` 本地开发
- `.env.production` 线上生产

启动时指定环境文件：

bash



运行







```
# 加载开发环境配置
node -r dotenv/config app.js dotenv_config_path=.env.development
```

配合 PM2 可在 `ecosystem.config.js` 配置环境文件，一键切换。

## 五、规范：.gitignore 必加

**严禁提交 .env 到代码仓库**，在 `.gitignore` 添加：

plaintext









```
.env
.env.*
!.env.example
```

新建 `.env.example` 作为模板，只保留配置 key、空值或示例，供团队复制使用：

env









```
# .env.example
PORT=
DB_HOST=localhost
DB_USER=
DB_PASS=
```

## 六、常用配套拓展

1. dotenv-expand

   

   支持环境变量嵌套引用：

env









```
BASE_URL=http://127.0.0.1:3000
API_URL=${BASE_URL}/api
```

1. dotenv-cli

   

   命令行直接指定 env 文件启动项目，不用改代码：

bash



运行







```
npx dotenv-cli -e .env.prod node app.js
```

## 七、优缺点

### 优点

1. 零侵入、轻量，仅几十 KB；
2. 统一管理敏感配置，避免明文硬编码；
3. 区分多环境，本地调试灵活；
4. 主流框架原生兼容：Express、Koa、NestJS、Vite、Webpack。

### 局限

1. `.env` 仅本地开发使用；**线上服务器优先使用系统环境变量**（云服务器、PM2、Docker、K8s 环境变量优先级更高）；
2. 纯文本存储，本地机器泄露仍有风险，不可用于极高密级密钥；
3. 浏览器前端无法直接读取（前端需打包注入，推荐 vite/env 等工具）。

## 八、与 PM2 配合使用流程

1. 本地开发用 `.env` 读取配置；
2. 线上生产不依赖 `.env`，在 `ecosystem.config.js` 写入 `env_production`；
3. PM2 启动时自动注入生产环境变量，安全且统一管理。

## 九、总结定位

dotenv 是 Node 项目**本地环境配置标准工具**，核心作用分离业务代码与敏感配置，是后端、全栈项目开发的基础依赖，常与 PM2 搭配完成「本地调试 + 线上进程托管」整套部署流程。





# 命令行测试接口

案例 post

```
curl -X POST http://127.0.0.1:3000/api/account/login -H "Content-Type:application/json" -d '{"account":"admin","password":"123456"}'     enter键
输出结果
{"code":200,"msg":"登录成功","data":{"id":1,"account":"admin","role":1,"company_id":null}}
```

# app.js启动了服务。如何检查是否启动，服务是否正常

# 套检查方案（按优先级执行，适配你的 Node app.js 项目）

## 一、方式 1：PM2 托管（你项目使用 ecosystem.config.js，推荐）

### 1. 查看进程是否存在

bash

```
pm2 list
```

- 看到 `sales-server` 且 `status: online` → 进程已启动
- 显示 `stopped` / 不存在 → 服务未运行

### 2. 查看进程详细状态、内存、重启次数

bash

```
pm2 show sales-server
```

重点看：

- `status`：online = 正常；errored = 启动失败
- `restart_time`：频繁重启 = 代码崩溃（之前的 502 根源）
- `script path`：确认启动文件是 app.js

### 3. 实时查看运行日志（判断服务是否能正常处理请求）

bash

```
pm2 logs sales-server --lines 500
```

- 无红色报错、有监听端口日志 `listening on http://127.0.0.1:3000` → 服务正常
- 持续抛出 `Cannot find module` / SQL 报错 / 异常堆栈 → 服务启动后会崩溃，访问接口 502

## 二、方式 2：原生 node app.js 直接启动（无 PM2）

### 1. 查找所有 node 进程，确认 app.js 是否在运行

bash

```
# 列出所有node进程
ps aux | grep node
# 过滤端口3000（你的后端监听端口）
lsof -i :3000
# 或
netstat -tlnp | grep 3000
```

#### 结果判断：

1. `lsof -i :3000` 有输出，显示 node 进程 PID → 服务启动并监听 3000 端口
2. 无任何输出 → 服务未启动 / 启动失败 / 端口未监听

### 2. 杀死残留卡死进程（端口占用时）

bash

```
# 拿到PID后强制结束
kill -9 进程PID
```

### 3. 前台运行直接看启动报错（最准）

bash

```
cd /var/www/selling-large-screens/sales-server
node app.js
```

- 控制台打印 `Server running on port 3000` → 启动成功
- 直接抛出红色 Error（如找不到模块、数据库连接失败）→ 启动失败

## 三、方式 3：端口连通性测试（验证服务能接收请求，核心校验）

### 1. 服务器本地自测（最准确）

bash

```
# 访问登录接口，有正常json返回=服务完全可用
curl http://127.0.0.1:3000/api/account/login -X POST -d "username=admin&password=123456"
```

- 返回 `code:200` / 正常业务 json → 服务运行正常，能处理接口
- `Connection refused` → node 服务未监听 3000 端口
- 直接断开 / 无响应 → 启动后内部崩溃

### 2. 公网 IP 跨机器验证（你现在 IP 能访问就是通过这个验证）

bash

```
curl http://8.1**.2.**/api/account/login -X POST -d "username=admin&password=123456"
```

## 四、方式 4：系统层面判断（进程被系统杀死场景）

### 查看是否内存溢出被内核 OOM 杀掉

bash

```
dmesg | grep -i "out of memory"
```

有输出 = 服务器内存不足，每次请求内存暴涨后系统直接杀掉 node 进程，表现为 “启动几秒后自动消失，接口 502”

## 五、最简一键排查流程（直接复制逐条执行）

bash

```
# 1. 查看PM2进程状态
pm2 list
# 2. 查看端口是否监听3000
lsof -i :3000
# 3. 本地curl测试接口可用性
curl http://127.0.0.1:3000/api/account/login -X POST -d "username=admin&password=123456"
# 4. 查看实时运行日志，排查崩溃报错
pm2 logs sales-server
```

## 六、结果总结判断标准

1. ✅ 完全正常：PM2 online + 3000 端口存在 + curl 接口返回 200 业务数据
2. ⚠️ 启动但异常：进程在线、端口存在，但 curl 请求后进程消失 / 日志抛错（你之前 dotenv 缺失就属于这类）
3. ❌ 未启动：pm2 列表无进程 /lsof 无 3000 端口 /curl 连接拒绝







# 关于域名

 域名访问项目报403

一、核心报错 1：`http://www.xiaorui.xyz/`、`favicon.ico` 返回 403 Forbidden

### 原因

1. **域名未完成 ICP 备案**：国内服务器 Nginx / 云服务商拦截未备案域名，直接返回 403，日志里`beian-block`（备案拦截）已佐证；
2. Nginx 静态资源权限不足：前端 dist 目录文件 / 文件夹权限为`0600`，nginx 运行用户无读取权限；
3. Nginx 防盗链 / IP 黑白名单限制访问。



