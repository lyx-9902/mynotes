# 浙政钉h5微应用开发vue

引自[参考](https://blog.csdn.net/weixin_48693596/article/details/117924655?spm=1001.2101.3001.6650.17&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-17-117924655-blog-120341532.235^v38^pc_relevant_sort_base2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-17-117924655-blog-120341532.235^v38^pc_relevant_sort_base2&utm_relevant_index=18)

## 1.在页面引入专有钉钉 JSAPI

```
npm install --save gdt-jsapi
import dd from 'gdt-jsapi'; /在使用页面导入
Vue.prototype.$zydd = zydd //或者挂载到vue 
<script src="https://g.alicdn.com/gdt/jsapi/1.9.6/index.js"></script> //CDN 引入
```

## 2.免登功能

```
 dd.getAuthCode({
      corpId:"xxxxx"//参数非必须 不传也行 
   }).then((res) => {
      if (res) {
         console.log(res.code)
         //取得免登code 调用登录api操作
         // ......
      }
   })
```

3.接入埋点
背景:应用上架需要接入监控 应省大数据局要求，现所有应用都需要接入监控。
埋点代码分为：稳定性监控代码（Emas）和流量分析代码(A+)；其中流量分析代码(A+)包含通用采集 SDK、基础埋点、用户信息埋点；稳定性监控代码（Emas）只需要在首页加入。流量分析代码(A+)每个页面都需要加入，也可以写通用js，在其他页面引入。

稳定性监控代码（Emas）

```
<script src='https://wpk-gate.zjzwfw.gov.cn/static/wpk-jssdk.1.0.2/wpkReporter.js' crossorigin='true'></script>
<script>
   try {
      constconfig = {
         bid: '************', //唯一标识 需要去开发者后台获取
         signkey: '1234567890abcdef',
         gateway: 'https://wpk-gate.zjzwfw.gov.cn'
      };
      constwpk = newwpkReporter(config);
      wpk.installAll();
      window._wpk = wpk;
   } catch (err) {
      console.error('WpkReporterinitfail', err);
   }
</script>

```

**流量分析代码(A+)** 每个页面引入 包括首页 可以封装成通用js

待定 存疑

查看上传成功
可在console里面的network里查看。
流量分析（A+）具体查看方法：参见‘浙政钉h5&小程序应用采集开发手册‘。 稳定性监控（Emas）可以查看：upload状态为200即为上报成功。

![](.\img\20210615151725932.png)

埋点成功查询链接
https://yida-pro.ding.zj.gov.cn/alibaba/web/APP_VTZ4TZZSGZXB37IUIUM6/inst/homepage/#/
每周一晚上更新 输入标识可查询是否成功 你这周埋的点可能要下周一晚才能查询是否成功

4.判断是否是浙政钉打开

```
let ua = navigator.userAgent.toLowerCase();
   	if(/taurusapp/.test(ua)){
   		
   	}
```

