`Houdini api`：可以自定义一个`css`属性，我们平常使用的`css`属性，例如：`font-size, background`，这些都是系统内置的；

所以可以使用`Houdini`去自定义一个`css`属性，让`css`属性可以去参与运行和计算，会去参与到渲染过程中

```css
@property --direc {  定义一个Houdini
  syntax: '<angle>';  允许接收的一个值
  initial-value: 0deg;  默认值
  inherits: false;  该属性是否可以被继承
}

使用也是跟变量的使用方法一样
var(--direc)
```



