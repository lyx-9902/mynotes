# 前端阿里云oss上传文件

技术点： vue项目，直接上传文件到阿里云存储桶。

优点： 上传服务端不限速，仅受客户端宽带影响。公司网络上传大文件测试约10M/s。

文档地址： 阿里云-》文档》阿里云对象存储OSS》开发参考》Browser.js （网页端js）

相关视频

https://www.bilibili.com/video/BV1Lm421M7TM/?spm_id_from=333.337.search-card.all.click&vd_source=08704ab849ba956e9d7acbdbd55b0991

## 操作步骤：



npm 插件

https://npmjs.com



ali-oss

```
npm install ali-oss --save
```



```

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <input id="file" type="file" />
    <button id="upload">上传</button>
    <script src="https://gosspublic.alicdn.com/aliyun-oss-sdk-6.18.0.min.js"></script>
    <script>
      const client = new OSS({
        // yourRegion填写Bucket所在地域。以华东1（杭州）为例，yourRegion填写为oss-cn-hangzhou。
        region: "yourRegion",
        authorizationV4: true,
        // 从STS服务获取的临时访问密钥（AccessKey ID和AccessKey Secret）。
        accessKeyId: "yourAccessKeyId",
        accessKeySecret: "yourAccessKeySecret",
        // 从STS服务获取的安全令牌（SecurityToken）。
        stsToken: "yourSecurityToken",
        // 填写Bucket名称。
        bucket: "examplebucket",
      });

      // 从输入框获取file对象，例如<input type="file" id="file" />。
      let data;
      // 创建并填写Blob数据。
      //const data = new Blob(['Hello OSS']);
      // 创建并填写OSS Buffer内容。
      //const data = new OSS.Buffer(['Hello OSS']);

      const upload = document.getElementById("upload");

      async function putObject(data) {
        try {
          // 填写Object完整路径。Object完整路径中不能包含Bucket名称。
          // 您可以通过自定义文件名（例如exampleobject.txt）或文件完整路径（例如exampledir/exampleobject.txt）的形式实现将数据上传到当前Bucket或Bucket中的指定目录。
          // data对象可以自定义为file对象、Blob数据或者OSS Buffer。
          const options = {
            meta: { temp: "demo" },
            mime: "json",
            headers: { "Content-Type": "text/plain" },
          };
          const result = await client.put("examplefile.txt", data, options);
          console.log(result);
        } catch (e) {
          console.log(e);
        }
      }

      upload.addEventListener("click", () => {
        const data = file.files[0];
        putObject(data);
      });
    </script>
  </body>
</html>

```





