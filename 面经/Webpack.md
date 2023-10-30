`Webpack`的核心概念：

* `entry`入口：`webpack`构建的第一步从`entry`开始，查找对应的入口文件，决定哪一个模块作为构建项目的起点
* `output`出口：告知`webpack`打包好后的代码如何进行命名以及路径位置
* `module`模块：在`webpack`中一切皆为模块，一个模块对应一个文件
* `chunk`代码块：一个`chunk`由一个或多个模块组合而成，用于代码的合并和分割
* `loader`转换器：`webpack`原生只支持加载`js`文件，有`loader`的使用，可以让`webpack`拥有加载非`js`文件的能力
* `plugin`插件：`webpack`构建过程中会广播出许多的事件，可以监听这些事件，利用`webpack`的`api`修改输出内容

`webpack`的基本功能

* 代码转换：可以将`ts`代码转为`js`代码，`less`转为`css`代码
* 文件优化：压缩`js / css / html`代码，压缩合并图片
* 代码分割：提取多个页面的公共代码
* 模块合并：将多个模块合并成为一个文件
* 自动刷新：监听本地资源的变化，自动刷新页面

`webpack`的构建流程

* 初始化编译参数：通过配置文件和`shell`语句或者读取合并参数
* 开始编译：根据上一步获取到参数，生成一个`compiler`对象，加载所有的配置的`plugin`，执行对象的`run`方法开始编译
* 确定入口：根据配置的`entry`找出入口文件，开始解析文件生成`AST`语法树
* 编译模块：调用所有的`loader`对模块进行编译，根据模块生成依赖关系图
* 输出资源：根据依赖关系图，组装成一个个包含多个模块的`chunk`，将`chunk`转为一个单独的文件加入输出队列中，根据配置路径输出文件名和路径

`loader`和`plugin`的区别
![img](https://img-blog.csdnimg.cn/b1b5c65dd961480a9a53ad8d22a2114e.png)

* 运行阶段：`loader`是在编译阶段运行，`plugin`是在整个周期都起作用
* `loader`需要下载，然后使用；`plugin`下载，引用，使用

如何利用`webpack`优化前端性能

* 代码压缩
* 按需加载：代码分割`splitChunks`，可以将`node_modules`中的代码单独打包成一个`chunk`输出；使用`dll`进行分包，`dll`可以将一些不常更新的框架和库进行单独打包；路由懒加载

如何提高`webpack`的构建速度

* 减少需要构建的代码或者文件；可以通过`HMR`热模块替换，热模块替换只会对发生变化的文件进行重新构建和替换；缩小文件的处理范围，合理利用`exclude`属性，减少不必要的文件检索；`babel`缓存：进行第二次构建的时候，会读取之前的缓存，只会重新构建发生变化的文件；`dll`分包
* 进行多进程打包；可以使用`thread-loader`

`webpack`打包优化：

优化构建速度：

* 优化搜索文件，缩小文件的搜索范围，可以合理的使用`include / exclude / test`；对匹配的文件进行分析转换，使用`module.noParse`指定哪些文件不需要进行分析转换；

* 避免重复编译第三方库，可以使用`DllPlugin / DllReferencePlugin / hard-source-webpack-plugin`，把第三方库单独打包到一个文件当中，这个文件是一个单纯的依赖库，依赖库不会跟随业务代码一起重新打包；

  ```javascript
  // npm i hard-source-webpack-plugin --save-dev 安装作为开发依赖
  const HardSourceWebpackPlugin = require('hard-source-webpack-plugin')
  chainWebpack: config => {
      config
        .when(process.env.NODE_ENV === 'development',  // 开发时使用
          config => {
            config
              .plugin('HardSourceWebpackPlugin')
              .use(HardSourceWebpackPlugin);
          }
        )
    },
  ```

* `happyPack / thread-loader`开启多线程`loader`转换，`loader`通常会读取整个文件，操作相对比较耗时，需要将`happyPack`任务分解成多个子进程来完成

  ```javascript
  config.module
    .rule('thread-loader')
    .test(/\.vue/)  // 针对vue文件
    .include.add(path.resolve("src"))  // 针对src目录下
    .end()
    .use({
      loader: "thread-loader",
      options: {
        workers: 6,  // 开启6个线程进行编译
      },
    })
    .loader('thread-loader')
  ```

* `paralleUglifyPlugin`开启多核压缩`js`文件

优化开发体验：

* 开启模块热替换`HMR`：只针对发生变化的模块进行编译，然后替换。

优化输出内容：

* `DefinePlugin`区分环境，减少生产环境代码体积
* 压缩`js`，压缩`css (mini-css-extract-plugin)`，压缩图片`(image-webpack-plugin)`
* `tree-shaking`删除无用的`js`代码
* 分离第三方库，通过`external`指定某一个些库不参与打包
* `gzip`压缩：`compression-webpack-plugin`