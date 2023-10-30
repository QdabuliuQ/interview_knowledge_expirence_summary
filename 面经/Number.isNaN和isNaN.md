`Number.isNaN`和`isNaN`的区别

`isNaN`：该函数会将接收的值进行判断，先**判断是否能够转为数字**，任何不能转为数字的值都会访问`true`

```javascript
isNaN(NaN)  // 本身就是NaN 返回true
isNaN("ABC")  // ABC字符串无法转为数字，所以返回 true
isNaN(123)  // 是一个数字，所以返回false
isNaN("123")  // 字符串123可以转为数字 所以返回 false
```

`Number.isNaN`：该函数**不会对接收到的值进行转换**，而是直接判断该值是否就是`NaN`

```javascript
Number.isNaN(NaN)  // true
Number.isNaN("ABC")  // ABC字符串不是 NaN 关键字 所以返回 false
```

`NaN`关键字不会和任何值相等，也就是`NaN === NaN`的结果为：`false`

```javascript
isNaN("0yd")  // true  无法转为数字 所以返回 true
isNaN("0xd")  // false  这是一个十六进制的值 可以转为数字  所以返回false

Number.isNaN("0yd")  // false  Number.isNaN会直接判断传入的值 是否是NaN 不会进行类型转换
Number.isNaN("0xd")  // false
```

