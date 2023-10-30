`esm`全称：`es module`；是`es6`提供模块导入导出的一种方式
`esm`中通过`import`导入模块，在文件当中通过`export`导出模块

```javascript
// main.js
import a from "a.js"
console.log(a)

// a.js
export let a = 1
```

也可以通过`script`标记创建一个`module`，`modole`当中的代码块会形成一个独立的作用域，不同`script`标签内的代码是无法相互访问

```html
<script type="module">
  import Vue from "url"
  ...
</script>
```

在`import`导入模块的时候，我们通常是使用相对路径或者绝对路径进行导入；我们也可以简化导入的方式，也就是直接通过：`import Vue from "vue"`的方式，如果想实现这种方式的导入，需要配合使用`import.map`

```html
<script type="importmap">
	{
		"imports": {
			"vue": "url"
		}
	}
</script>
<script type="module">
  import Vue from "vue"
</script>
```

`import.meta`保存的是当前模块的上下文元数据；

* `import.meta.url`获取当前模块的`url`路径
* `import.meta.scriptElement`返回是浏览器特有的元属性