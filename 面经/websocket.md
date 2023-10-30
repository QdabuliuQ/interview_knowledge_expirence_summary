`WebSocket`最大的特点就是服务器可以主动推送消息给客户端，客户端也可以发送消息给服务器，实现双向平等对话；并且`websocket`没有同源限制，可以和任意服务器进行通信

```javascript
let ws = new WebSocket("ws://xxxx.com")
// websocket打开
ws.onopen = function() {}

// websocket收到消息
ws.onmessage = function(){}

// websocket关闭
ws.onclose = function() {}
```

`ws`存在4种状态`readyState`：`Connecting 0`连接中，`Open 1`连接成功，`Closing 2`连接正在关闭，`Closed 3`连接已关闭

`send`方法主动向服务器发送数据，`close`方法关闭连接