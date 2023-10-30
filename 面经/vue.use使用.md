`vue.use`通常是用于安装一些引入的第三方库，例如有组件库；
`use`方法接收一个对象或者一个函数，如果是一个对象的话，那么对象内部必须包含一个`install`方法，如果是函数，则会作为`install`函数直接执行。
`install`函数接收到第一个参数就是`vue`实例

```javascript
const demo = {
	// 参数为对象时，需要提供install方法
    install: (Vue) => {
        console.log('自定义插件', Vue);
        // 定义一些vue中常用的全局方法
		Vue.prototype.$Toast = () => { console.log('全局toast提示') }; // toast提示,通过this.$Toast调用
		Vue.prototype.$request = () => { console.log('全局request请求') }; // request请求,通过this.$request调用
    }
}
export default demo;

import demo from './lib/demo';
Vue.use(demo); // 安装自定义插件
```

