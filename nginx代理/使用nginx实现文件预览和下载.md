  需求： 实现一个文件下载的链接



```
文件位置：C:/myapk/myapp.apk
```

   关键配置：

```
  server {
    listen 8080;
    server_name localhost;
    location / {
        root   C:/myapk;
        autoindex on;
    }
  }
```



使用：

   浏览器地址   127.0.0.1:8080/myapp.apk     触发下载

