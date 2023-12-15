# uni-app 微信版改造浙政钉H5手机端



## 背景

原项目： uniapp + 微信开发工具 == 发布成微信小程序

功能包含了手机获取经纬度信息，持续获取位置信息，拍照，录像，录音，api主要偏向微信。 例如wx.startLocationUpdateBackground， 

## 改造记录

第一步：配置模板

![](.\img\微信截图_20231019140251.png)

参考官网https://uniapp.dcloud.net.cn/collocation/manifest.html#h5-template

## 第二步 安装辅助插件

平时web开发时，在手机上，如果是要看控制台信息，都需要alert弹窗，这样很不友好.还会阻拦进程。

通过vConsole.js 重写console方法，实现了类似于微信小程序的移动端调试效果。

具体使用方法也很简单

```xml
<script src="https://cdn.bootcdn.net/ajax/libs/vConsole/3.9.0/vconsole.min.js"></script>
    <script>
        // init vConsole
        var vConsole = new VConsole();
        console.log('Hello world');
    </script>
```

[https://www.npmjs.com/package/vconsole](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2Fvconsole)

 vue可以npm安装  

main.js文件配置

```

import VConsole from 'vconsole';
 new VConsole();
```

第三步：安装浙政钉api

```
执行
npm install gdt-jsapi

main.js中引入
import dd from 'gdt-jsapi'
console.log(dd)// 项目中可以直接使用dd.xx方法；
```

[其他浙政钉配置参考](https://blog.csdn.net/weixin_48693596/article/details/117924655?spm=1001.2101.3001.6650.17&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-17-117924655-blog-120341532.235%5Ev38%5Epc_relevant_sort_base2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-17-117924655-blog-120341532.235%5Ev38%5Epc_relevant_sort_base2&utm_relevant_index=18)



参考链接

[使用 uni-app 打包 H5](https://blog.csdn.net/weixin_50339217/article/details/125260027?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-1-125260027-blog-133807399.235^v39^pc_relevant_anti_vip_base&spm=1001.2101.3001.4242.2&utm_relevant_index=4)



[uniApp 打包H5工程 超详细（打包-实现跨域-nignx配置）](https://blog.csdn.net/qq_20236937/article/details/124258970?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-124258970-blog-133807399.235^v39^pc_relevant_anti_vip_base&spm=1001.2101.3001.4242.1&utm_relevant_index=3)





