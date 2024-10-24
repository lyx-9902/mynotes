问题记录  摘自网上



## 分包

在开发小程序前，最好先根据自己开发的功能模块或其他逻辑做好分包，不然后期在上传代码时报错才发现这个问题，再去分包就很麻烦。小程序限制每个包不超过2M，可以分9个子包，总包大小不超过20M。



在pages.json中添加subPackages数组，切记要放在pages后面，否则无法生效。



体验版缓存问题





uni.navigateTo改为uni.navigateBack



详情查看：

https://zhuanlan.zhihu.com/p/664751392