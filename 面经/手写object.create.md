手写`object.create`函数；`object.create`函数会创建一个新的对象，并且传入的对象会作为新创建的对象的`__proto__`

```javascript
Object.prototype.myCreate = function(p) {
  function F() {}  // 创建临时构造函数
  F.prototype = p
  return new F()
}
let obj = {
  a: 'a',
  b: 'b'
}
let a = Object.myCreat(obj)
console.log(a.a, obj.a)  // a a
a.c = 'c'
console.log(a.c, obj.c)  // c undefined
```

