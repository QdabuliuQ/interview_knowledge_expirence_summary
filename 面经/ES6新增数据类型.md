`ES6`新增的数据类型

* `Symbol`基本数据类型，`Symbol`函数会返回一个`symbol`值，并且是唯一的

* `BigInt`是一种内置的对象，可用于表示大于`2^53-1`的整数

* `Set`集合，引用类型数据，如果使用`instanceof`检测返回的是`Object`，集合一组值，与数字类似，可以存储引用类型的数据，可以被`for ... of`遍历

* `Map`哈希表，存在`key - val`的映射关系，`key`可以是引用类型的数据，可以被`for ... of`遍历

* `WeakMap / WeakSet`弱映射不是可迭代对象，只实现了`get / set / has / delete`；`key`只能为引用类型的值，`value`可以是任意类型

  ```javascript
  let map = new WeakMap()
  map.set(1, '2')  // 报错 valid value used as weak map key
  // 键必须是引用类型
  map.set(() => {}, '2')
  ```
  
