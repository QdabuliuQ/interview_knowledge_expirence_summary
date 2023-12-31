介绍一下`http2.0`

`http2.0`是`http1.1`的升级改造，相对于`http1.1`新增几个特性

1. 二进制协议，在`http1.1`中，头信息和数据体都是`ascii`或二进制，而在`http2.0`中，头信息和数据体都必须是二进制
2. 数据流的概念，`http2.0`的数据包不是按照顺序进行发送，同一个连接里面连续的数据包，属于不同的请求，所以每一个请求或者响应的所有数据包都成为数据流
3. 多路复用，`http2.0`实现了多路复用，同一个连接里面客户端和服务器可以同时发送和响应多个请求，不用按照顺序一一返回，避免了队头堵塞的问题
4. 头信息压缩，`http2.0`对`http`头信息进行了压缩，减少带宽的浪费，使用`gzip / compress`进行压缩
5. 服务器推送，`http2.0`可以主动向客户端推送信息