`Cookie`：由于`http`协议是无状态的，对于事务处理没有记忆的功能，也就是每次客户端和服务器会话完成后，服务器是不会保存任何会话信息。所以每一个请求都是独立的，服务器无法确认当前的访问者的身份信息，所以就需要一个状态，来告知服务端是谁发起了该请求；

* `cookie`是存储在客户端，`cookie`是服务器发送给客户端，并且保存在浏览器中的一小段数据，它会随着下一次请求，携带发送给服务端

* `cookie`是不可跨域的，每一个`cookie`都会绑定单一的域名，所以在别的域名下无法使用

* `cookie`可以设置`samesite`属性，用于防止`CSRF`攻击；`samesite`属性值有三个：`strict / lax / none`

  * `strict`：完全禁止第三方获取`cookie`，只有当前网页的`url`和请求目标完全一致的时候，才会带上`cookie`，这个规则过于严格，会造成不好的用户体验；
  * `lax`：防范跨站，大多数情况下是禁止获取`cookie`，除了`get`请求，例如：链接，预加载，`get`表单可以获取`cookie`
  * `none`：设置`none`的时候必须同时设置`secure`才能够生效
  
  | 属性       | 值                                                           |
  | ---------- | ------------------------------------------------------------ |
  | name=value | cookie的名称以及相对于的值                                   |
  | domain     | cookie所属的域，默认是当前域名                               |
  | path       | 指定cookie在哪个路径在生效                                   |
  | maxAge     | cookie的失效时间，如果为负数，则是临时cookie，关闭浏览器失效，否则cookie会在maxAge秒后失效 |
  | expires    | 过期时间，在某个时间点后cookie会失效                         |
  | secure     | cookie是否使用安全传输协议进行加密传输                       |
  | httpOnly   | 设置httpOnly后，cookie无法通过JS脚本读取                     |

`Session`：是记录服务器和客户端会话状态的机制，`session`是存储在服务器端，`sessionId`会存储在客户端的`cookie`中

`cookie`和`session`的区别：

1. `session`相对于`cookie`来说更加安全，因为`session`是存储在服务器端，`cookie`存在客户端
2. 存取值类型不同，`cookie`只支持字符串数据，`session`可以存任意数据类型
3. 有效期不同，`cookie`可以设置过期时间，`session`客户端关闭后失效
4. 存储大小不同，`cookie`一般大小为`4k`，`session`存储的容量远大于`cookie`，但也会造成占用过多服务器资源

`token`：访问资源接口的资源凭证，`token`组成：`uuid`用户身份标识，`time`当前时间戳，`sign`签名

* 服务器端无状态，支持移动设备，更加安全；
* 客户端发起登录接口请求，服务器接收到后验证账号密码，两者无误后，根据查找到的用户信息，生成一个`token`返回给客户端，后续请求都需要携带`token`放在请求头`Header`中，服务器端收到`token`会进行解密，判断用户信息以及是否有效。

`JWT`：`JSON Web Token`，是一种认证授权机制，跨域认证的方案；用户登录成功后，服务器端会根据用户信息生成`jwt`返回给客户端，后续客户端请求需要从`header`请求头的`Authorization`中添加`jwt`；服务器接收到请求后，也会从`Authorization`中获取`jwt`并进行解密
`jwt`包含了三个部分：`header / payload / signature`；三部分用`.`分割，`payload`通常是用户的信息加密后的内容

`token`和`jwt`的区别：

相同：

* 都是访问资源的身份认证信息
* 都可以记录用户的信息
* 使服务器端无状态化
* 只有认证成功后，才能够访问服务器上受保护的资源

不同点：

* `token`：服务器校验客户端发送过来的`token`时，需要到数据库中查询用户信息，然后才进行验证
* `jwt`：服务器只需要使用密钥解密进行校验即可，不需要查找数据库或者减少数据库查询

`token`可以存储在`localStorage / sessionStorage / cookie`当中；
存储在`localStorage / sessionStorage`中，这样很容易受到`xss`攻击，通过代码注入的方式，读取到存储在`webStorage`中的`token`
存储在`cookie`中，可以通过设置`httponly`防止被`js`脚本读取