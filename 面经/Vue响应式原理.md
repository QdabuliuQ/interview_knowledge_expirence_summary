创建`class Vue`，在构造函数中接收`obj_instance`配置对象；从配置对象中读取`data`对象保存到`$data`。`Observer`监听数据，`Compile`解析模板。

```javascript
class Vue {
  // obj_instance 传入的配置对象
  constructor(obj_instance) {
    // 将data属性保存到 $data
    this.$data = obj_instance.data
    Observer(this.$data)  // 添加数据监听
    Compile(obj_instance.el, this)
  }
}
```

`Observer`给对象的子属性添加监听；通过`Object.defineProperty`，遍历`Object.keys`遍历对象每一个属性。然后递归`Observer`监听每一个属性；手动添加上`get / set`方法，并且在`set`中可能接收一个新的对象，这个对象也需要添加上监听，所以也需要进行递归。

```javascript
// 给data_instance添加监听
function Observer(data_instance) {
  // 递归停止条件
  if(!data_instance || typeof data_instance !== 'object') return
  // 遍历每一个对象的属性
  Object.keys(data_instance).forEach(key => {
    let value = data_instance[key]  // 保存值
    Observer(value)  // 递归监听
    Object.defineProperty(data_instance, key, {
      enumerable: true,  // 是否可遍历
      configurable: true,  // 是否可配置
      get() {
        return value
      },
      set(newValue) {
        value = newValue  // 修改value值
        Observer(newValue)  // 新值也需要进行劫持
      },
    })
  })
}
```

`Compile`模板解析，将模板的内容当中的差值表达式`{{}}`替换成真实的数据。通过正则表达式匹配`{{}}`；如果当前的节点是文本节点，则需要查找是否存在差值表达式，然后将值取出，从`vm.$data`中获取数据，修改`node.nodeValue`进行数据替换。

```javascript
function Compile(element, vm) {
  vm.$el = document.querySelector(element)  // 获取根dom元素
  const fragment = document.createDocumentFragment()  // 创建文档碎片
  let child;
  while(child = vm.$el.firstChild) {
    fragment.append(child)  // 加入到文档碎片
  }
  fragment_compile(fragment)
  const pattern = /\{\{\s*(\S+)\s*\}\}/  // 匹配差值表达式
  function fragment_compile(node) {
    if(node.nodeType === 3) {  // 文本节点
      const xxx = node.nodeValue
      const result_regex = pattern.exec(node.nodeValue)  // 匹配差值表达式
      if(result_regex) {
        const arr = result_regex[1].split('.')
        // 读取属性值
        const value = arr.reduce(
          (total, current) => total[current], vm.$data
        )
        node.nodeValue = xxx.replace(pattern, value)
      }
    }
    // 递归遍历子节点
    node.childNodes.forEach(child => fragment_compile(child))
  }
  vm.$el.appendChild(fragment)  // 将文档碎片加入到dom
}
```

`Dependency`类负责收集依赖，`Watcher`负责监听，然后触发对应的函数去更新视图。
`Dependency`存在`subscribers`数组，存放`watcher`实例对象，其中有`notify`方法，如果当数据的`set`触发的时候，可以调用`notify`方法去修改所有使用到该数据的视图。

```javascript
class Dependency {
  constructor() {
    this.subscribers = []
  }
  addSub(sub) {
    this.subscribers.push(sub)  // 将watcher实例对象加入
  }
  notify() {
    // 调用更新函数 去更新视图
    this.subscribers.forEach(sub => sub.update())
  }
}

class Watcher {
  constructor(vm, key, callback) {
    this.vm = vm
    this.key = key
    this.callback = callback  // 视图更新的回调函数
    Dependency.temp = this  // 保存当前实例
    // 获取属性值触发get函数
    key.split(".").reduce((total, current) => total[current], vm.$data)
    // temp置空  上面触发了get方法 已经将实例保存进入 subscribers 数组
    Dependency.temp = null 
  }
  update() {
    const value = this.key.split(".").reduce(
    	(total, current) => total[current], this.vm.$data
    )
    this.callback(value)  // 将变化后的值传入函数 更新视图
  }
}
```

当`compile`解析的时候，如果遇到文本节点，并且出现差值表达式的时候，进行替换，这个时候需要给这个节点添加更新视图的回调函数，通过`new Watcher(vm, result_regex[1], newValue => {})`

```javascript
// 创建订阅者
new Watcher(vm, result_regex[1], newValue => {  // 执行回调函数更新视图
  node.nodeValue = xxx.replace(pattern, newValue)  // 将节点文本替换
})
```

当获取节点的时候，也就是触发`get`拦截器的时候，添加依赖，将`Dependency.addSub`监听进去。
修改值的饿时候，也就是触发`set`拦截器的时候，需要更新视图，也就是调用`dependency.notify`更新视图

```javascript
get() {
  // 添加依赖 将实例加入到 sub 数组当中
  Dependency.temp && dependency.addSub(Dependency.temp)
  return value
},
set(newValue) {
  value = newValue  // 修改value值
  Observer(newValue)  // 新值也需要进行劫持
  dependency.notify()  // 通知 更新视图
}
```

`Observer`给数据添加监听`-> Compile`解析模板替换数据`-> Dependency`收集依赖，数据变化的使用调用`notify`更新视图`-> Watcher`监听实例，`compile`的时候给结点创建`watcher`实例，加入到`dependency`；

```javascript
class Vue {
  // obj_instance 传入的配置对象
  constructor(obj_instance) {
    // 将data属性保存到 $data
    this.$data = obj_instance.data
    Observer(this.$data)  // 添加数据监听
    Compile(obj_instance.el, this)
  }
}

// 给data_instance添加监听
function Observer(data_instance) {
  const dependency = new Dependency()  // 创建依赖
  // 递归停止条件
  if(!data_instance || typeof data_instance !== 'object') return
  // 遍历每一个对象的属性
  Object.keys(data_instance).forEach(key => {
    let value = data_instance[key]  // 保存值
    Observer(value)  // 递归监听
    Object.defineProperty(data_instance, key, {
      enumerable: true,  // 是否可遍历
      configurable: true,  // 是否可配置
      get() {
        // 添加依赖 将实例加入到 sub 数组当中
        Dependency.temp && dependency.addSub(Dependency.temp)
        return value
      },
      set(newValue) {
        value = newValue  // 修改value值
        Observer(newValue)  // 新值也需要进行劫持
        dependency.notify()  // 通知 更新视图
      },
    })
  })
}

// 解析函数 对模板进行解析将模板的差值表达式替换成数据
function Compile(element, vm) {
  vm.$el = document.querySelector(element)  // 获取dom
  const fragment = document.createDocumentFragment()  // 创建文档碎片
  let child;
  while(child = vm.$el.firstChild) {
    fragment.append(child)  // 加入文档碎片
  }
  fragment_compile(fragment)
  // 解析每一个节点
  function fragment_compile(node) {
    const pattern = /\{\{\s*(\S+)\s*\}\}/  // 匹配差值表达式
    if(node.nodeType === 3) {  // 文本节点
      const xxx = node.nodeValue
      // 正则匹配返回数组
      const result_regex = pattern.exec(node.nodeValue)
      if(result_regex) {
        const arr = result_regex[1].split(".")  // 获取嵌套对象属性
        const value = arr.reduce(  // 获取嵌套的属性
          (total, current) => total[current], vm.$data
        )
        node.nodeValue = xxx.replace(pattern, value)  // 将节点文本替换
        // 创建订阅者
        new Watcher(vm, result_regex[1], newValue => {  // 执行回调函数更新视图
          node.nodeValue = xxx.replace(pattern, newValue)  // 将节点文本替换
        })
      }
    }
    // 递归处理子节点
    node.childNodes.forEach(child => fragment_compile(child))
  }
  vm.$el.appendChild(fragment)  // 将碎片文档加入
}

// 依赖 收集和通知订阅者
class Dependency {
  constructor() {
    this.subscribers = []  // 订阅者数组
  }
  addSub(sub) {  // 将watcher实例加入到数组
    this.subscribers.push(sub)
  }
  notify() {  // 遍历所有的实例 调用 update 方法更新视图
    this.subscribers.forEach(sub => sub.update())
  }
}

// 订阅者
class Watcher {
  constructor(vm, key, callback) {
    this.vm = vm
    this.key = key
    this.callback = callback
    // 将当前实例保存到Dependency的temp属性当中
    Dependency.temp = this
    // 获取属性值触发get函数
    key.split(".").reduce((total, current) => total[current], vm.$data)
    // temp置空  上面触发了get方法 已经将实例保存进入 subscribers 数组
    Dependency.temp = null 
  }
  update() {  // 更新
    // 获取新值 传递给callback函数
    const value = this.key.split(".").reduce(
      (total, current) => total[current], this.vm.$data
    )
    this.callback(value)  // 调用callback函数去更新视图
  }
}
```



