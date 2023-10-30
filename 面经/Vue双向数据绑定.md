Vue双向数据绑定

Vue2使用的是`Object.defineProperty`来对对象的子属性进行响应式的绑定，对`data`属性进行深度优先遍历，确保每一个属性都能够绑定上`getter / setter`，通过`getter / setter`拦截操作，触发视图更新

Vue3使用的`Proxy`代理对象，`Proxy`是`ES6`的新特性，可以对一个对象进行监听，参数一：监听的对象；参数二：配置选项；配置选项：`get 获取对象属性触发，set 修改对象属性触发，has 进行 propKey in proxy触发，deleteProperty 删除对象属性触发 ...`