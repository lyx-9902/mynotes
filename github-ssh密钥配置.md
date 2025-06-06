命令工具： powershell兼容较好



github上的项目，本地克隆的方式，分为三种，一种https,一种ssh。 

  https较为简单，直接克隆即可，提示的话输入账号和密码。

  当https出现网络安全等问题，不能使用的时候，可以使用ssh,但需要一点配置。

 配置方法如下：

 思路是：本地通过指令生成密钥， github上创建一条密钥， 线上和本地相呼应，验证身份。

### 1. 检查 SSH 密钥是否存在

```shell
ls -al ~/.ssh 或  ls ~/.ssh
# 查看是否有 id_rsa.pub 或 id_ed25519.pub 文件

有的话，会显示 .ssh的目录位置   C:\Users\Lenovo\.ssh
id_ed25519.pub文件，记事本形式打开，复制出来。 
```

### 2. 生成新的 SSH 密钥（如果没有）

```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
# 按照提示完成密钥生成，建议使用默认路径和密码 

your_email@example.com邮箱，就是你github注册绑定的邮箱号。
```

### 3 登录github  settings>SSH keys

  点击  NEW SSHKEY按钮， 起个名字， 把刚才复制的密钥，复制进去。点击 保存。



### 4 测试本地是否联通

终端输入`ssh -T git@github.com`测试SSH连接

### 5 若连接成功

则终端输入`git clone github复制的SSH地址`即可下载项目到本地





## 其他参考：

SSH方式
打开终端，输入ssh-keygen -t rsa -b 4096 -C "your_email@example.com回车生成SSH密钥（可ls ~/.ssh查看是否生成成功）
将公钥添加到github设置中：github中settings -> SSH and GPG keys -> New SSH key 保存即可（公钥通常保存在用户主文件夹/.ssh/id_rsa.pub，用户主文件夹即打开终端对话框初始文件夹，私钥通常保存在用户主文件夹/.ssh/id_rsa。也可终端输入cat ~/.ssh/id_rsa.pub查看公钥，cat ~/.ssh/id_rsa查看私钥）
终端输入ssh -T git@github.com测试SSH连接（如果没有建立连接，删除密钥，重复1-2步）。
若连接成功，则终端输入git clone github复制的SSH地址即可下载项目到本地。
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。

原文链接：https://blog.csdn.net/weixin_49240038/article/details/144462345









