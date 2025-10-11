# 项目自启动的实现

项目背景： 

   vue项目，打包dis文件后，nginx部署前端项目， 需求： win笔记本，开启自启动。



##  实现方法1：

 win11, 本案例中，vue项目部署后，双击nginx.exe启动。   思路为： 把nginx.exe复制一个快捷方式，剪切到win系统的启动文件夹中。 测试可以。



使用命令快速的打开用户自启动的目录：

win+R键打开运行窗口，输入shell:startup,回车即可快速打开。（冒号是英文的冒号哦）

作用是： win系统，开机是，会把启动文件夹中的程序，逐个启动。

C:\Users\Lenovo\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup



## 实现方法2

#### 实现思路：

   nginx.ext需要双击的操作，  替换为   ==》  编写一个start.bat批处理文件。 ==》然后，把批处理文件，转化为win系统的服务。



详细步骤：

####  1.下载WinSW

####   2.创建xml配置文件

      ```xml
<service>
<id>WinSW-x64-NginxService</id>
<name>aaaaluyunxiaodenginxbackserve</name>
<description>nginxbackserveDescription</description>
<executable>F:\test-robot\nginx-1.24.0\start.bat</executable>
</service>


参数说明：

id：用于唯一标识一个服务。
name：定义服务在Windows服务管理器中显示的名称。
executable：指定服务要运行的可执行文件路径。
arguments：设置传递给可执行文件的参数。
logmode：指定日志记录的方式，例如"rolland"表示日志文件会滚动。
onfailure ：定义服务失败时采取的行动，如重新启动服务。

      ```
    
      ```

#### 3

将winSW.exe文件，和xml配置文件，放置到nginx的文件夹同一级目录。 原因：是，xml指令执行需要使用winsw辅助程序， 而start.bat执行脚本的执行代码中，需要依赖RunHiddenConsole.exe辅助程序。 保持同一个执行根节点。

#### 4

管理员权限打开shell . 把自己的服务初始化进win系统中， 然后启动自己的服务。

shell进入winSW.exe所在文件夹下，执行命令。

```
cd F:\test-robot\nginx-1.24.0
```



常用指令：

```
 Get-Service -Name WinSW-x64-NginxService  获取自己的服务的状态信息 ，是否保活中，还是停止了  
 
 Status   Name               DisplayName
------   ----               -----------
Running  WinSW-x64-Nginx... aaaaluyunxiaodenginxbackserve
```

WinSW-x64NginxService.exe这个是我服务bat 起的名字。

```
 .\WinSW-x64NginxService.exe install 初始化服务
 
 .\WinSW-x64NginxService.exe start  启动服务
 
  .\WinSW-x64NginxService.exe stop  停止服务
  
  .\WinSW-x64NginxService.exe uninstall 卸载服务
 
 .\WinSW-x64NginxService.exe status 查看当前服务的状态   Active (running)表示运行中
```

####  5. 操作完毕



 本案例碰到的问题：

​     install初始化成功， start服务成功后，随即失败。  

   但是查看进程页面中，  nginx已经启动了。   并且检查start.bat脚本，测试正常。

 原因：

- 如果服务启动后立即停止，可能是批处理文件执行完成后自动退出，可尝试修改 start.bat 文件，在最后添加 `timeout /t -1` 阻止批处理脚本退出

   ```js
   @echo off
   set nginx_home=F:\test-robot\nginx-1.24.0
   ```

echo Starting nginx...
%nginx_home%/RunHiddenConsole %nginx_home%/nginx.exe -p %nginx_home%

echo Nginx started. Press Ctrl+C to exit.   新增部分
timeout /t -1 >nul    新增部分
```

### 修改说明：

1. **新增等待命令**：`timeout /t -1 >nul` 会使批处理脚本无限期等待，直到用户手动按下 `Ctrl+C` 终止
2. **隐藏超时提示**：`>nul` 用于隐藏 `timeout` 命令的倒计时提示信息
3. **添加提示信息**：`echo Nginx started. Press Ctrl+C to exit.` 告知用户如何终止脚本



这样修改后，当服务通过 WinSW 启动时，批处理脚本不会自动退出，从而保持 Nginx 进程运行。
```





## 拓展：

WinSW将执行文件服务化 

https://blog.csdn.net/liangmengbk/article/details/148103295









## 2025.10.11日记

自启动的改进版，

1. 上边记录的是如下的执行逻辑。

 winsw.exe + xml ==>  执行 start.bat + RunHiddenConsole.exe   ==》执行启动nginx.exe应用程序

2.改进版逻辑

 winsw.exe + xml ==>  执行启动nginx.exe应用程序

xml的执行路径修改为 nginx.exe即可。 

```xml
<service>
    <id>nginx</id>
    <name>nginx</name>
    <description>nginx server</description>
    <logpath>%BASE%\logs</logpath>
    <logmode>roll</logmode>
    <depend></depend>
    <arguments></arguments>
    <startmode>Automatic</startmode>
    <executable>%BASE%\nginx.exe</executable>   //executable  可执行的
    <stopexecutable>%BASE%\nginx.exe -s stop</stopexecutable>
</service>
```















   