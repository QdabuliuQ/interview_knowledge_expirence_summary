`PerformanceObserver`是`web api`，可以实现对页面的性能的分析。通常用于对页面加载进行评估

```javascript
let pb = new PerformanceObserver((list) => {
  // 触发信息
  let {
    duration,
    startTime
  } = list.getEntriesByName("first-contentful-paint")[0]
  console.log(list.getEntriesByName("first-contentful-paint"));
  console.log(duration + startTime);
})  // 创建实例对象

pb.observe({  // 对页面的初始加载 监听
  entryTypes: [
		'paint'
	]
})
```

首屏加载分为多个阶段：`first paint -> first contentful paint -> first meaningful paint`

![QQ20210608-214622@2x.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/34904e1dc80649aea1e7fc6d1cc711a7~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)