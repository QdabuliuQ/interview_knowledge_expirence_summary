`dom`解析的过程：
1.将载入的`html`文件解析成`dom`树，并且将各个标签解析成`dom`树的各个节点，解析`html`的同时会将`css`样式解析成`css`规则
2.将解析成`dom`树和`css`规则进行关联生成渲染树`render tree`
3.进入布局阶段，通过生成的`render tree`，给每一个`dom`进行页面布局
4.布局接收就会调用浏览器的`ui`接口对页面进行绘制

为了提高页面的呈现速度，渲染引擎采用的是渐进式渲染，也就是边解析，边渲染的模式进行

`DOMContentLoaded / onload`事件的区别
`DOMContentLoaded`事件主要是在`dom`加载完毕之后触发，不包括样式表，图片资源；
而`onload`事件是要求`dom`，图片，脚本，样式表都加载完毕之后才会触发；
所以`DOMContentLoaded`总会比`onload`先执行