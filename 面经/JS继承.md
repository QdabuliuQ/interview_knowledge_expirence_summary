原型链继承：通过`prototype`实现继承，可以继承父类的属性和方法；`prototype`值为父类的实例对象，这种方法可以成功继承父类的属性和原型上的属性。
缺点：如果父类成员存在引用类型的属性，那么会共享，更改的其中一个，会影响所有。子类实例不能够父类构造函数进行传参。

```javascript
function Son() {}
function Father() {
  this.kill = []
  this.say = () => {
    
  }
}
Father.prototype.fun = function() {}
// 将父类的实例对象作为子类的prototype值
Son.prototype = new Father()
// 修改构造函数指向
Son.prototype.constructor = Son

let s1 = new Son()
s1.say()  // 可以调用父类继承过来的方法
s1.fun()  // 可以调用父类的原型上的方法
s1.kill.push('学习')

let s2 = new Son()
s2.kill  // ['学习'] 引用类型共享了
```

构造函数继承：通过在子类中调用父类的构造函数，同个`apply`修改父类的`this`指向，指向的是子类的`this`，这样就可以将父类的属性绑定到子类当中；**相对于原型链继承，引用类型的属性不会被共享，每一个子类都是独立的；并且可以给父类传递参数**
缺点：无法继承父类的原型上的属性和方法

```javascript
function Father() {
  this.kill = []
}
Father.prototype.fun = function() {}
function Son() {
  Father.apply(this)
}

let s1 = new Son()
s1.kill.push("学习")
s1.fun()  // 子类无法访问父类原型上的属性和方法

let s2 = new Son()
s2.kill  // []  引用类型不会存在共享 是独立的
```

组合式继承：将原型链继承和构造函数继承合并；解决了引用类型的属性冲突问题，解决了无法继承父类原型上的属性和方法的问题。
缺点：这里会调用了两次`Father`类，这样会存在重复的属性，存在性能上的问题；

```javascript
function Father() {}
function Son() {
  // 实例对象上存在 Father 的属性
  Father.apply(this)  // 构造函数继承
}
// 实例对象的 __proto__ 也会存在 Father 属性 会出现重复的属性
Son.prototype = new Father()  // 原型链继承
Son.prototype.constructor = Son
```

寄生组合继承：组合继承的升级，子类的`prototype`继承的是父类的`prototype`；解决了重复调用`Father`父类带来的性能问题，以及重复的属性

```javascript
function Father() {}
function Son() {
  Father.apply(this)
}
const FN = function() {}  // 创建一个函数
FN.prototype = Father.protoype  // 函数的prototype指向父类的原型对象
Son.prototype = new FN()  // 子类的prototype指向新创建的对象
Son.prototype.constructor = Son
```

`class`继承：`es6`的方式实现继承，通过`extends`关键词实现父类和子类的继承关系

```javascript
class Father {
  constructor() {
    this.kill = []
    this.say = function() {}
  }
}
class Son extends Father {}  // 子类继承父类

let s1 = new Son()
let s2 = new Son()
```



