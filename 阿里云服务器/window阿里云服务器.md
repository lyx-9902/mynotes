# 阿里云win服务器的使用

  本地使用的是win电脑。

1. 前提条件**：

   - 实例已[绑定](https://help.aliyun.com/zh/ecs/user-guide/instance-logon-credential-management#939ea2f00ekaf)公网IP或[弹性公网IP](https://help.aliyun.com/document_detail/417420.html)；

   - 已设置实例登录密码；

   - 安全组已放行RDP端口（默认3389），建议仅允许您的本地IP访问以提升安全性

     。

1. 本地 Windows 系统连接（最常用）
   1. 按`Win+R`打开运行窗口，输入`mstsc`回车，启动远程桌面工具。
   2. 在 “计算机” 栏输入服务器公网 IP，点击 “连接”。
   3. 弹出登录窗口后，输入用户名`Administrator`和之前设置的服务器密码，首次连接会出现证书安全警告，点击 “是” 信任，等待片刻即可进入服务器桌面。