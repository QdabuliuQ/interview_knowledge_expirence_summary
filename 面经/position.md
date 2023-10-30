`position`属性值

* `static`：`position`属性的默认值，当我们修改`left / right / top / bottom`的时候是无效的
* `relative`：相对定位，修改`left / right / top / bottom`的时候是根据其本身来计算位置偏移
* `absolute`：绝对定位，脱离正常的文档流，元素相对于其最近的非`static`的父元素进行定位
* `fixed`：固定定位，它可以相对于屏幕视口进行定位
* `sticky`：粘性定位，是`relative`和`fixed`的接口，当元素距离页面边界的阈值的时候，就会触发`fixed`