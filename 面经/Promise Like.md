`Promise Like`是`Promise A+`规范，也就是说先有`Promise A+`规范，再有`ES6`的`Promise`；所以我们只要遵循`Promise A+`规范，就可以实现将其作为`Promise`一样进行使用

```javascript
$.ajax()  // 在 jq 的 ajax 函数返回的并不是一个 promise，但其却可以通过 await 来进行使用
await $.ajax()  // 主要是因为返回的内容是符合 promise A+ 规范，才被运行这么使用
```

`Promise A+`规范要求：

* 必须是一个对象或者一个函数
* 以及必须有`then`属性，并且属性值是函数

所以我们就可以编写`isPromiseLike`函数进行判断，判断传入的内容是否符合`Promise A+`规范

```javascript
function isPromiseLike(obj) {
  // obj必须是对象或者函数，以及其必须有then方法
  return obj && (typeof obj === 'object' || typeof obj === 'function') && typeof obj.then === 'function'
}
```

