Promise

什么是`Promise`？
`Promise`是异步编程的一种解决方案；`promise`是一个对象，可通过`new Promise`创建一个`promise`实例对象，`Promise`接收一个`execute`函数，该函数内部执行的一般是一个异步任务，函数同时会收到两个参数：`resolve / reject`，通过调用两个参数函数，从而决定`promise`的状态，`promise`的状态有三种：`pending 等待 / fulfilled 成功 / rejected 失败`；一旦`promise`的状态改变，就确定下来，也就是状态凝固，后续是无法进行修改。

`promise`和`async`有什么区别
1.`async`函数串行的写法形式彻底解决了异步回调的问题，并且`async`函数的语义相对于`promise`更加明确；`promise`是链式调用，可能会造成代码语义不明确；`async`使用同步的写法，异步的效果
2.`async`函数是基于`Promise`实现和生成器函数`Generator`同步写法

为什么`promise`是微任务队列，`setTimeout`是宏任务队列？
宿主线程的回调就是宏任务队列，`setTimeout`，网络请求；`js`的回调就是微任务队列；归浏览器管的属于宏任务。