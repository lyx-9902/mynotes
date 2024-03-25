## 知识点：

#### 1.快应用：

快应用是九大手机厂商基于硬件平台共同推出的新型应用生态。用户无需下载安装，即点即用，享受原生应用的性能体验。

# uni-app 开发微信小程序

`uni-app`是一个使用`Vue.js` 开发所有前端应用的框架，开发者编写一套代码，可发布到`iOS`、`Android`、`H5`、以及各种小程序（微信/支付宝/百度/头条/QQ/钉钉）等多个平台。

即使不跨端，`uni-app`同时也是更好的小程序开发框架

![image-20210420143058763](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\image-20210420143058763.png)

我使用`uni-app`框架主要用来开发微信小程序，我使用过程中感觉的好处是：

- `uni-app`框架使用的开发工具 `HBuilderX`，`HBuilderX` 内置相关环境，开箱即用，无需配置`nodejs`， 需要什么插件可直接下载，测试、打包、发布特别方便。
- `uni-app`采用`Vue.js`语法，基本支持`vue`大部分语法（`vue`的动态组件`component`不支持）。
- `PC`端使用`vue`封装的一些`js`方法，以及建构思想，可直接移植到`uni-app`中，比如：本人`pc`项目中`api`接口`js`文件，可直接复制到小程序框架`api`文件夹中（PS：`api`文件夹维护后端请求路径）
- `uni-app` 周边生态丰富，[插件市场](https://ext.dcloud.net.cn/)可用的组件特别多，也可使用vue语法自己封装一些组件。

## 开发工具（HBuilderX）

- `HBuilderX`: [官网IDE下载地址](https://www.dcloud.io/hbuilderx.html);
- `HBuilderX`是通用的前端开发工具，但为`uni-app`做了特别强化。
- `HBuilderX`提供了一些插件，可直接下载安装，具体如下图： `工具` > `插件安装`

一、uniapp介绍
1.uniapp做混合开发的好处：

2. 开发环境&IDE工具：
二、使用步骤
第一步：打开HBuilderX选择文件->新建项目->选择uniapp项目
第二步：配置manifest.json文件，配置微信小程序AppID
第三步：小程序开发工具配置服务代理，端口
第四步：点击运行->运行到小程序模拟器
第五步：点击发布->选择小程序发布
第六步：小程序开发工具中填写对应的信息->上传->公众平台上提交审核














