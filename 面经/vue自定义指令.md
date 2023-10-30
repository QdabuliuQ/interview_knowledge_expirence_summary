`vue`提供了自定义配置指令，一般指令是用于需要对`dom`完成修改或者操作的场景下使用；
指令又分为了局部指令和全局指令，全局指令可以整个`vue`项目当中使用

指令注册

```javascript
// 全局指令注册
app.directive("指令名称", {
  // 配置对象
})
<input v-指令名称 />
  
// 局部指令注册
const defineDir = {
  focus: {
    // 配置对象
  }
}
export default {
  directive: defineDir
}
```

在`vue2`中指令同样也是存在生命周期，随着指令挂载的`dom`元素的创建和销毁；生命周期函数：`created / beforeMounted / mounted / beforeUpdate / updated / beforeUnmounted / unmounted`；

```javascript
const autoFocus = {
  focus:{
    created(){
     	console.log('created');
    },
    beforeMount(){
     	console.log('beforeMount');
    },
    mounted(el){
     	console.log('mounted');
    },
    beforeUpdated(){
     	console.log('beforeUpdated')
    },
    updated(){
     	console.log('updated');
    },
    beforeUnmount(){
     	console.log('beforeUnmount');
    },
    unmounted(){
     	console.log('unmo`unted');
    }
  },
}
```

钩子函数中会传递参数：`el 指令所绑定的dom元素`，`binding 指令的所有信息`；
`binding`属性包含：`arg 自定义指令参数，value 自定义指令绑定的值`

```
v-example:foo.bar="baz"
{
  arg: 'foo',
  modifiers: { bar: true },
  value: /* `baz` 的值 */,
  oldValue: /* 上一次更新时 `baz` 的值 */
}
```