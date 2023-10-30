`Vue3`相对于`Vue2`的改进

* 响应式系统的改进：`Vue2`使用的时候`defineProperty`，给对象的每一个子属性添加`getter / setter`函数，通过递归调用，确保对象的每一个子属性都能够绑定上监听函数；`Vue3`使用`proxy`来代替`defineProperty`，因为`proxy`的性能优于`defineProperty`，`proxy`可以拦截属性的访问，修改等操作，可以监听到对象属性的增加和删除，数组长度的变化，这些都是`defineProperty`无法做到的
* 编译优化：标记静态节点，这样在进行`diff`算法更新的时候可以跳过静态节点，提升性能
* `fragment`：模板里面可以不用创建唯一的根标签，可以有多个根标签
* `composition API`：组合式`api`相对于`Vue2`的`Option API`来说更加灵活，可以根据实际开发需求自由搭配