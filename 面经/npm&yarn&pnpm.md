`npm`：在`npm1 / npm2`中的依赖结构是嵌套关系，依赖存在子依赖，则会嵌套放入`node_modules`当中，子依赖也会存在`node_modules`。
缺点：存在大量重复的依赖，占用磁盘空间大，在安装依赖的时候也需要重复的安装，层级嵌套深，会导致文件路径太长，`window`的文件路径存在限制。
![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0e1e2d8158d5419ca5be8c9ddd96b4c6~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

`yarn`：对于`npm1 / npm2`存在的问题，`yarn`能够一定程度上进行解决，`yarn`通过扁平化的管理解决`npm`依赖层级嵌套的问题。例如通过`yarn`安装`express`，`yarn`会将`express`的子依赖都同意平铺在`node_modules`下，这样解决`npm`依赖嵌套过深的问题，并且相同版本的包也不会重复的安装，解决公共依赖的问题。
![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/43d844fee1124a63a8756bba71cdd8f1~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

`npm3`也采取了和`yarn`一样的扁平化的方案，但扁平化的管理也存在许多的问题。

* 扁平化算法耗时较长
* 多个版本的依赖包，只会提升一个，其他版本还是会放在依赖的`node_modules`下
* 项目中可以非法访问未声明的依赖包，幽灵依赖的问题。

幽灵依赖：在`package.json`中未声明的依赖，却可以在代码中引入，这些依赖是依赖的子依赖，因为其可以在`node_modules`中找到，存在一定的安全隐患，如果某天将该依赖删除，那么其子依赖也会删除，这样就会影响代码的运行。

针对幽灵依赖的问题，`pnpm`解决了该问题；
`pnpm`：是通过软硬链接的方式，所以依赖的子依赖都是放在`.pnpm`文件夹下，这些依赖都全是通过全局的`store`硬链接过来的，包和包之间的结构关系是通过软链接；通过这种方式，依赖都是去全局的`store`查找，避免重复安装，也避免幽灵依赖的问题，直接子依赖都是放在`node_modules`下，依赖的子依赖都是放在`node_modules / .pnpm`下，通过`依赖名称@版本号`进行命名。
**项目的 `node_modules` 下不再是各种被铺平的依赖，而是与 `package.json` 中声明的依赖基本保持一致，结构清晰了也解决了幽灵依赖的问题。**
![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6db906f4f5d843d5bca6fafccfb6c285~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)