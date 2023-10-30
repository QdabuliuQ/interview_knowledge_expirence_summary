`flex`布局也叫弹性布局，目标是提供一个更好更快捷的布局方式。
`flex`布局是一个完整的模块，它包含了一套完整的属性，采用`flex`布局的元素，称为`flex`容器，容器当中的子元素称为`item`项目。
![Flexbox布局.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bb462fbbab1f4dfca38b871571af7091~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

`flex`布局存在两条轴，分别是：水平轴`main axis`，垂直轴`cross axis`；项目默认是以水平轴进行排列。
![Flexbox布局-主轴.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bbbad88b6c9d4a22a82da2e5f0c21f0c~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

`main axis`是主轴；`main start - main end`是主轴的开始位置和结束位置。
`cross axis`是交叉轴；`cross start - cross end`是交叉轴的开始位置和结束位置

有两种方式可以开启`flex`布局，分别是：`display: flex / inline-flex`，两者的区别是：如果子元素是块元素，则可以使用`flex`，如果子元素是行内元素，则可以使用`inline-flex`

`flex-direction`属性：控制主轴的方向，可以设置为`row / row-reverse / column / column-reverse`；

* `row`是默认值，从左到右进行排列，主轴仍然是横向。
  ![Flexbox布局-flex-direction.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b8122d1fc3014d9db734ca6ad6bd189f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

* `row-reverse`：主轴任然是横向，但是从右到左进行排序

* `column`：主轴方向是纵向；从上到下

  <img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/06998644245049dcbd7b5dc4b2841a73~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp" alt="Flexbox布局-flex-direction2.png" style="zoom:50%;" />

* `column-reverse`：主轴方向是纵向，方向相反，从下到上

`flex-warp`：容器是否可以换行显示，默认有三个值：`nowarp / warp / warp-reverse`

* `nowarp`：默认值，也就是默认不换行，元素会在一行排列
* `warp`：换行显示
* `warp-reverse`：换行显示，不过第一行是在最下面

`justify-content`：元素在主轴的对齐方式；有六个属性值：`flex-start / flex-end / center / space-between / space-around / space-evenly`

* `flex-start`：元素在主轴的左侧/上侧对齐
* `flex-end`：元素在主轴的右侧/下侧对齐
* `center`：元素在主轴的中间对齐
* `space-between`：元素两端对齐，元素间隔相同
* `space-around`：中间元素间隔相同，两端元素间隔是中间元素的一半
* `space-evenly`：所有元素的间隔都相同

`align-items`：元素在交叉轴的对齐方式；有五个属性值：`flex-start / flex-end / center / baseline / stretch`

* `flex-start`：元素在交叉轴的上侧/左侧对齐
* `flex-end`：元素在交叉轴的下侧/右侧对齐
* `center`：元素在交叉轴居中对齐
* `stretch`：默认值

`order`：定义项目在容器中排列顺序，数值越小越靠前；
`flex-basis`：定义项目在容器中的宽度
`flex-grow`：定义项目的放大比例，默认值是`0`![Flexbox布局-第 4 页6.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ea54a8cb618b4c35881c6b1548dc878b~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)
`flex-shrink`：定义项目的缩小比例，当宽度不够的时候就按`shrink`进行缩小
![Flexbox布局-第 4 页3.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/dea7c53d3eeb4287b4765a20436c47a4~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)