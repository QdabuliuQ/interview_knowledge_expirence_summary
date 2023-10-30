`MAX_SAFE_INTEGER `：在`js`中表示最大安全整数，如果超出该数，那么可能在进行数据运算上，会出现错误；其值就是`2 ^ 53 - 1`；

```
MAX_SAFE_INTEGER + 1 == MAX_SAFE_INTEGER + 2  // true
```

`MAV_VALUE`：表示`js`里能够表示的最大数值

`js`中的数是通过`IEEE 754`标准的双精度浮点数来表示；

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/5/30/17263be557add8c8~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.awebp)

`sign`是符号位，`exponent`是指数位，`fraction`是小数点后的部分；`js`采用64位浮点数来表示数字，指数部分和尾数部分占11位和52位，Number类型可以表示的最大值就是53位二进制，也就是2^53-1