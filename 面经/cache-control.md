`cache-control`是`http1.1`提出的缓存控制策略；在`cache-control`中有几种常见的配置：

* `max-age`：表示强制缓存的有效期，单位是`s`
* `no-cache`：表示不会进行强制缓存，而是进行协商缓存，每次都会先去服务器查询资源是否发生了改变
* `no-store`：禁止强制缓存和协商缓存，直接拉取新的资源
* `private`：如果设置了该字段，则缓存不会被`CDN`缓存，`CDN`失效，每次只能访问源服务器
* `public`：`CDN`服务器可以访问

`no-cache`是禁止强制缓存，而`no-store`是禁止所有缓存

缓存的位置：`memory cache / disk cache`

* `memory cache`：从浏览器的内存空间`RAM`中读取信息，读取速度快，生命周期短
* `disk cache`：从磁盘中存取，读取速度慢，可以持久存储