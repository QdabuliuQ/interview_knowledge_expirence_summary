`Rest`：`Representational State Transfer`，表现层状态转移
`URL`中只使用名词来定位资源，用`http`协议里的动词`(get / post / put / delete)`来实现增删改查的操作

比如，我们有一个friends接口，对于“朋友”我们有增删改查四种操作，怎么定义REST接口？

* 增加一个朋友，`uri: generalcode.cn/v1/friends` 接口类型：POST
* 删除一个朋友，`uri: generalcode.cn/va/friends` 接口类型：DELETE（在http的`parameter`指定好友id）
* 修改一个朋友，`uri: generalcode.cn/va/friends` 接口类型：PUT（在http的parameter指定好友id）
* 查找一个朋友，`uri: generalcode.cn/va/friends` 接口类型：GET

以上定义的接口`url`都是不包含动词，也就是符合`REST`协议；
`generalcode.cn/va/deleteFriends`，如果是这种接口，则不符合`REST`规范，因为存在`delete`动词

```
Restful风格
看Url就知道要什么
看http method就知道干什么
看http status code就知道结果如何
```

