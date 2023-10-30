`React`和`Vue`的区别

* `React`提倡的是单向数据流，`Vue`默认支持的双向数据绑定
* `Vue`虚拟`dom`在渲染过程中，会跟踪每一个组件的依赖关系，不需要重新渲染整个组件树；`React`当组件状态改变的时候，全部的子组件都会重新渲染，可以通过`shouldComponentUpdate / pureComponent`来控制
* `Vue`支持`template`模板写法，类似于常规的`html`目标，`React`推荐使用`jsx`
* `Vue`通过`getter / setter`精准知道数据的变化，触发对应的视图更新，`React`是通过比较引用的方式进行
* `Vue`的构建工具：`vue-cli`，`React`构建工具：`create react app`