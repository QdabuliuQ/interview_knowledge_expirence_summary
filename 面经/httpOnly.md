什么是`httponly`

`httpOnly`是`cookie`的一种状态，了解`httponly`之前必须先知道`cookie`；
`cookie`是浏览器可以保存的一些`tokenId`信息，用于区别用户身份，`cookie`大小只有`4k`左右，只能存储少量的信息；同时`cookie`是有限制的，超过时间限制，就会被系统删除，通过`cookie`存储在浏览器，会被修改的风险，可以通过打开浏览器控制台进行修改
`httponly`是包含在`Set-Cookie`的`http`响应头文件中的附加标志，生成`cookie`的时候使用`httponly`标志，这样`cookie`是无法浏览器端通过`js`进行修改，也就是当一个`cookie`的选项被设置为`httponly = true`的时候，`cookie`只能通过服务器来进行修改
也就是通过`document.cookie`是无法获取到设置为`httponly`的`cookie`，自然也就是无法修改