由于`JavaScript`语言采用的是单线程的，所以所有任务只能在一个线程上完成，一次只能完成一件事情；前面的任务没有作完，后面的任务就必须等待。
`webworker`就是为`javascript`创建多线程，两个线程互不干扰。通常是`webworker`完成一些复杂的计算任务，然后将计算结果返回给主线程
`webworker`中是无法操作`dom`，也没有`window / document`，但可以使用`location / navigator / XMLHttpRequest`

* `new Worker("./worker.js")`创建一个`worker`对象，传入`worker.js`文件，当`worker`收到消息时触发执行

* 主线程通过`postMessage`进行消息传递，传递的数据可以是任意数据类型

* 主线程通过`onmessage`监听`worker`返回的消息

  ```javascript
  worker.onmessage = function() {}
  ```

* 主线程可以通过`terminate / close`关闭线程

* 在`worker`中通过`addEventListener`添加监听函数；`self.postMessage`发送消息

  ```javascript
  self.addEventListener("message", function() {
    self.postMessage()
  })  // 收到消息回调
  ```

* 在`worker`中可以通过`importScripts`导入其他脚本文件

  ```javascript
  importScripts('script1.js', 'script2.js');
  ```

  