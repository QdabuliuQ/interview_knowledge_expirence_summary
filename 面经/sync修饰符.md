当子组件需要修改`props`的时候，默认`vue`支持单向数据流的概念，子组件不允许在内部修改`props`，需要在父组件中修改，所以需要发送自定义事件到父组件，在父组件中进行修改

```javascript
// 子组件
this.$emit('update:title',newTitle)

<text-document
  v-bind:title="doc.title"
  v-on:update:title="doc.title=$event"
></text-document>
```

`.sync`是一个语法糖，可以简化以上的写法

```vue
<text-document v-bind:title.sync="doc.title"></text-document>
```

这样子组件改变`props`值的时候是在父组件中改变；而不是在子组件内部