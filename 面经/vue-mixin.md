`mixin`：`mixin`并不是`vue`专属，而是一种思想，类似于`hook`，可以将一些公共的代码进行抽离，`mixin`提供了一种非常灵活的方式，分发`vue`组件中可复用的功能，`vue`组件提高了代码的复用性，`mixin`是再逻辑代码上进一步进行抽离

```javascript
// src/mixin/index.js
// 创建一个mixin文件，其内容是一个对象，对象中的属性可以跟option api中一致
export const mixins = {
  data() {
    return {};
  },
  computed: {},
  created() {},
  mounted() {},
  methods: {},
};
```

使用`mixin`就需要先导入，然后放入`mixins`数组选项中即可混入

```javascript
import { mixins } from "./mixin/index";
export default {
  name: "App",
  mixins: [mixins],
}
```

如果`mixin`和组件中属性和方法冲突的时候，则默认使用组件内部定义的属性和方法