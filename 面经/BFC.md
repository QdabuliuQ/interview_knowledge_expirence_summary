什么是`BFC`？
`BFC`块级格式上下文，`block formatting context`，是一个独立的渲染区域，隔绝了内部和外部的联系，内部渲染不会影响外部。

如果创建`BFC`？

* 根元素`html`标签默认就会开启`BFC`
* `float`属性设置为`left / right`；
* `position`属性设置为`absolute / fixed`；
* `display`属性设置为`inline-block / flow-root / flex / table-caption`；
* `overflow`属性设置为`hidden / scroll / auto`

`BFC`应用场景

* 解决兄弟元素之间的`margin`重叠问题，可以给其中一个元素设置为`BFC`，就可以避免该问题；
* 清除浮动，如果子元素设置了`float`，那么父元素无法计算浮动子元素的高度，所以就会高度塌陷，可以通过开启`BFC`，`BFC`容器当中计算高度的时候浮动元素也会参与计算
* `margin`塌陷的问题，如果第一个子元素设置`margin-top`，那么很有可能会导致影响父元素的`margin-top`，所以可以给父元素开启`BFC`，从而解决该问题
* 如果目前该元素被后面的浮动元素遮挡了，那么可以将该浮动元素设置为`BFC`，避免被后面的兄弟浮动元素覆盖