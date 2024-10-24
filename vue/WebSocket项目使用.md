# webSocket项目使用



注意点：

1.请求头的加参数形式

2.易错点： 请求路径和传参字段

```javascript
let protocols = ["177"];
let ws = new WebSocket(`ws://192.168.112.4:8888/imchat/im/websocket/user/${protocols[0]}`, protocols);


ws.onopen = function (event) {
    console.log('连接已建立');
   
         console.log("发送一次消息");
        let msg = {
            "toId": 1,
            "sendType": 1,
            "content": '121212你谁啊',
        }
        ws.send(JSON.stringify(msg)); 
};


ws.onmessage = function (event) {
    console.log("onmessage",event);
    const message = event.data;
    console.log('接收到消息：', message);
};
ws.onerror = function (event) {
    console.log("onerror",event);
    console.error('发生错误：', event);
};
ws.onclose = function (event) {
    console.log("onclose",event);
    if (event.wasClean) {
        console.log('连接已关闭，关闭码：' + event.code + '，原因：' + event.reason);
    } else {
        console.error('连接意外关闭');
    }
};
```

