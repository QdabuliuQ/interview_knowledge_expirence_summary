`reactive`和`ref`的区别

* `ref`可支持的基本数据类型或者对象类型，`reactive`默认支持的是复杂数据类型，如果使用`reactive(10)`，这样会报警告；
* 通过`ref`定义的数据和`reactive`定义的数据，在数据获取上有点区别，`ref`定义的数据需要额外加上`.value`，而`reactive`不需要