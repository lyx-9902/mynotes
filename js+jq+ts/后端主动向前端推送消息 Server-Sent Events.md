## [后端主动向前端推送消息 Server-Sent Events](https://www.cnblogs.com/colin220/p/14455881.html)

任务： 

1 . WebSocket

2.  浙江掌上公路     app专门用于pc对手机端的呼叫   涉及：  各推 和小鱼的api

3. 文档型: 对掌上公路 对比目前的微信小程序，还缺少那些功能模块。 

   

知识点： 

#### 轮询 

轮询是在特定的的时间间隔（如每1秒），由浏览器对服务器发出[HTTP请求](https://baike.baidu.com/item/HTTP请求/10882159)，然后由服务器返回最新的数据给客户端的浏览器。

缺点：显然这样会浪费很多的带宽等资源

## 解决方式

WebSocket  定义

[HTML5](https://baike.baidu.com/item/HTML5)定义了WebSocket协议，能更好的节省服务器资源和带宽，并且能够更实时地进行通讯

**WebSocket**是一种在单个[TCP](https://baike.baidu.com/item/TCP)连接上进行[全双工](https://baike.baidu.com/item/全双工)通信的协议。WebSocket通信协议于2011年被[IETF](https://baike.baidu.com/item/IETF)定为标准RFC 6455，并由RFC7936补充规范。WebSocket [API](https://baike.baidu.com/item/API)也被[W3C](https://baike.baidu.com/item/W3C)定为标准



WebSocket 是独立的、创建在 TCP 上的协议。

Websocket 通过[HTTP](https://baike.baidu.com/item/HTTP)/1.1 协议的101状态码进行握手。

为了创建Websocket连接，需要通过浏览器发出请求，之后服务器进行回应，这个过程通常称为“[握手](https://baike.baidu.com/item/握手)”（handshaking）。







