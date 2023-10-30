`webpack`的`chunk`是将多个模块打包进一个`chunk`；最终的打包输出产物单位。
`chunk`涉及到`entry / optimization`等配置

在生成`seal`阶段，`webpack`会根据模块依赖图的内容组织分包。

* 同一个`entry`下触达的模块组织成一个`chunk`
* 异步模块单独组织为一个`chunk`
* `entry.runtime`单独组织成一个`chunk`

`entry`分包处理，对于不同的`entry`，`webpack`会创建不同的`chunk`进行打包；

```javascript
module.exports = {
  entry: {
    main: "./src/main",
    home: "./src/home",
  }
};
```

这里就会打包生成出两个`chunk`，分别是：`chunk[main] / chunk[home]`
![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b001227baf6943c8a19ad68900ae2c80~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)
通过构建的关系依赖图发现：如果`main`当中`import`了其他的依赖，那么就会将这些依赖继续打包进入`chunk[main]`当中，包括依赖的子依赖。
![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a842770d983f4d42a265cf859a63e3ac~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

异步模块分包处理，通过异步语句导入`require.ensure / import()`都是属于异步模块，这种情况会为这些模块单独创建一个`chunk`，然后将其子模块都打包进该`chunk`；同步模块中导入异步模块，使用`__webpack_require__.e`方法进行导入

`runtime`分包处理，可以根据业务需求将不同的模块打包进入同一个`chunk`

```javascript
module.exports = {
  entry: {
    index: { import: "./src/index", runtime: "solid-runtime" },
    home: { import: "./src/home", runtime: "solid-runtime" },
  }
};
```

这里形成了：`index.js / home.js / solid-runtime`三个`chunk`；`index / home`会打包进入`solid-runtime`当中
![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6ca2f6e814954ee198ff40c763be24a2~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)