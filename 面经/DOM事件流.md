DOM事件流

`DOM`事件流`(event flow)`存在三个阶段：事件捕获，事件处理，事件冒泡
![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1ee44735e4034d59979ab9e76c3de3f3~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp?)
事件捕获是从`document`开始向内层进行移动，而事件冒泡是从目标元素向外层进行移动，方向是相反的。也就是说先进行事件捕获，然后再进行事件冒泡

`addEventListener`函数用于给`dom`元素添加事件监听，第一个参数是监听的事件，第二个参数是监听的回调函数，第三个参数`(useCapture)`可以传一个布尔值，用于决定是否进行在事件捕获阶段执行，默认是`false`

事件委托也叫事件代理，利用的事件冒泡，子元素的点击事件会冒泡到父元素上，前提是该父元素也绑定了相同的事件，那么可以在父元素上统一监听所以子元素的事件，只需绑定一次即可，例如需要给`1000`个按钮绑定点击事件，如果通过`for`循环逐个遍历进行绑定，那么性能上很差，如果统一上父元素上进行一次绑定，在父元素上进行处理即可
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5bc4b224e0a94d5a86f221252d13322d~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp?)
此处给三个元素都绑定了两个事件，一个是捕获阶段执行，一个是冒泡阶段执行，执行顺序：`big capture -> center capture -> small capture -> small bubble -> center bubble -> big bubble`

什么是事件？
事件指的是用户在操作网页时发生的交互动作，比如`click / move`，除了用户手动触发的动作之外，也可以是文档加载，窗口滚动，都会触发对应的事件

什么是事件模型？
当前浏览器中一共有三种事件模型，1、`DOM0`级事件模型，这种模型不会事件传播，没有事件流的概念；2、`IE`事件处理，该模型存在两个过程，事件处理阶段和事件冒泡阶段，这种模型通过`attachEvent`来添加监听函数；3、`DOM2`级事件模型，该模型有三个过程：事件捕获，事件处理和事件冒泡，通过`addEventListener`来添加监听函数