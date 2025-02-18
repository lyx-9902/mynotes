#  web项目引入扣子智能体当AI客服

应用背景： web网页经常见右下角有一个客服机器人，特别是一些销售课程，旅游等，随着AI智能体的发展，实现上有了一个更简单的方法。例如： 扣子智能体。

 

 什么是扣子（Coze）1
国内地址：https://www.coze.cn

外网地址：https://www.coze.com

扣子是新一代 AI 应用开发平台。无论你是否有编程基础，都可以在扣子上快速搭建基于大模型的各类智能体，并将智能体发布到各个社交平台、通讯软件或部署到网站等其他渠道。


  操作步骤：

## 第一步： 用扣子创建一个智能体

   创建智能体，里面可以编排的东西太多了，自行百度。

   

## 第二步：发布智能体





<img src=".\img\sdk截图.png" style="zoom:80%;" />



 按照如下案例， 把代码放到body里，右下角即可出现客服会话小图标。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    测试



    <script src="https://lf-cdn.coze.cn/obj/unpkg/flow-platform/chat-app-sdk/1.1.0-beta.3/libs/cn/index.js"></script>
    <script>
        new CozeWebSDK.WebChatClient({
            config: {
                bot_id: '7472589258520936500',
            },
            auth: {
                type: 'token',
  token:'pat_yfy4n9fVVvNnivs5tTpIrNL9fRDpK9n2ayCLmgHbR88YQV2imT20UJtpr7iiF6Mw',
                onRefreshToken: async () => '',
            },
            componentProps: {
                title: '智能客服',
            },
            footer: {
                isShow: true,
                expressionText: 'Powered by &',
                linkvars: {
                    name: {
                        text: 'A',
                        link: 'https://www.test1.com'
                    },
                    name1: {
                        text: 'B',
                        link: 'https://www.test2.com'
                    }
                }
            }
        });
    </script>
</body>

</html>
```

如果报如下错误，是因为  参数不对。 Non-Token is unsupported; auth's type must be token

可以参照  扣子API >Chat SDK  

![](.\img\运行demo.png)

