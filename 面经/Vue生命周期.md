`Vue3`的生命周期：

1. `setup`：开始创建组件之前，在`beforeCreate / created`之前执行，创建`data / method`
2. `onBeforeMount`：挂载组件之前执行
3. `onMounted`：挂载组件后执行
4. `onBeforeUpdate`：组件更新之前执行
5. `onUpdate`：组件更新之后执行
6. `onBeforeUnmount`：组件卸载之前执行
7. `onUnmounted`：组件卸载后执行
8. `onActivated`：被包裹在`keep-alive`组件的子组件可以使用的生命周期函数，被激活时执行
9. `onDeactivated`：组件隐藏时候执行
10. `onErrorCaptured`：捕获组件内部错误

`Vue2`生命周期：

1. `beforeCreate`
2. `create`
3. `beforeMount`
4. `mounted`
5. `beforeUpdate`
6. `updated`
7. `beforeDestroy`
8. `destroyed`
9. `activated`
10. `deactivated`
11. `errorCaptured`

`vue2`中的`beforeCreate / create`声明周期函数在`vue3`中用`setup`替换