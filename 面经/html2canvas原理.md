`html2canvas`库是可以将网页内容输出为`png / jpg`格式图片，可以实现网页截图功能。

* `html2canvas`是利用`svg`的`foreignObject`标签，将`dom`内容放入`foreignObject`内部

  * `foreignObject`允许包含不同的`xml`命名空间的元素，也就是我们可以将`dom`节点作为`foreignObject`插入到`svg`节点中

    ```
    <svg xmlns="http://www.w3.org/2000/svg">
     <foreignObject width="120" height="50">
         <body xmlns="http://www.w3.org/1999/xhtml">
           <div>测试测试</div>
         </body>
       </foreignObject>
    </svg>
    ```

* 然后获取`svg`结构将该`svg`插入到`canvas`当中

* 最后`canvas`通过调用`drawImage`将`canvas`中的内容导出成为`png / jpg`

![html2canvas-foreignObject-flow.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2a648d5e202b488883fb13623d0972ca~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=576&h=934&s=43397&e=png&b=ffffff)