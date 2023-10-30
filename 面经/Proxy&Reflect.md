`Vue3`实现数据响应式是通过`Proxy / Reflect`来实现，`Vue2`实现数据响应式是通过`Object.defineProperty`来实现；

为什么`Vue3`要使用`Proxy / Reflect`
相对于`Vue2`，`defineProperty`存在很多的不足之处；

1. `defineProperty`需要给每一个属性都添加上`get / set`劫持函数，当一个对象层级嵌套很深的时候，就需要不断递归的调用，有多个属性就会创建多少个回调函数去处理；
2. `defineProperty`无法拦截到数组长度变化；所以`Vue2`又在内部重写数组的方法；
3. 无法拦截对象属性的新增，因为新增的属性没有通过`defineProperty`创建，所以自然也就没有响应式，需要手动调用`$set`方法

而这些问题在`Proxy`中都可以很轻松的解决，`Proxy`代理的是一整个对象，不需要对对象的属性逐个进行遍历，提高效率；以及不需要给每一个属性创建`get / set`回调函数，节省内存消耗；`Proxy`可以拦截到数组长度变化和对象属性添加和删除。

```javascript
let p = new Proxy(obj, {
  get: function(target, key, receiver) {
    return target[key]
  },
  set: function(target, key, value, receiver) {
    target[key] = value
  },
  deleteProperty: function(target, key) {
    delete target[key]
  }
})
```

在`Vue3`中不止使用`Proxy`，也使用了`Reflect`；`Reflect`的用法和`Proxy`很像。

```javascript
get(target,key,receiver){
    return Reflect.get(target,key,receiver)
},
set(target,key,val){
    Reflect.set(target,key,val)
},
deleteProperty(target,key){
    return Reflect.deleteProperty(target,key)
}
```

为什么要使用`Reflect`？

1. 为了在触发代理对象的劫持时，保证正确的`this`上下文指向；在`Proxy`的`get`函数参数中存在`receiver`代理对象，所以使用`Reflect.get(target, key, receiver)`将`receiver`进行传递；将内部的`this`指向的是`receiver`
2. 提高框架的健壮性；如果通过`defineProperty`重复定义一个属性的时候，会报错，这个时候我们需要不断通过`try ... catch`方法来捕获错误；而使用`Reflect.defineProperty`重复定义属性的时候，如果已经存在重复的属性，不会报错，而是返回`false`，表示定义失败；