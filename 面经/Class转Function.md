通过`es6`的`class`会经过转换，转换为`es5`的构造函数

```javascript
class Example {
  constructor(name) {
    this.name = name
  }
  func() {
    console.log(this.name)
  }
}

// 转为ES5构造函数
// 1.需要使用 use strict
"use strict"
function Example(name) {
  // 2.class不允许直接调用 只能直接通过 new 调用
  if(!(this instaceof Example)) {  // 不属于 Example 实例
    throw new TypeError("class只能通过new调用")
  }
  this.name = name
}
// 3.成员方法不能被枚举 通过defineProperty定义属性 enumerable 设置为 false
Object.defineProperty(Example.prototype, "func", {
  value: function() {
    // 4.成员函数不能通过new的方式调用
    if(!(this instanceof Example)) {
      throw new TypeError("成员函数不能通过new调用")
    }
  },
  enumerable: false  // 不可枚举
})
```

