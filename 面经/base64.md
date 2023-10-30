什么是`base64`？
`base64`是网络中最常见的用于传输的字节码的编码方式，`base64`就是基于`64`个**可打印字符**来表示二进制数据的方法
![img](https://img-blog.csdn.net/20180313122446386?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjA1NDUzNjc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

如果想要将某一个字符转为`base64`，则需要经过以下的步骤

1. 获取字符的`ascii`，转为`2`进制，然后每6个`bit`划分成为一组
2. 如果三个字符，则划分出`4`组，然后每组高位补`0`
3. 然后转为`10`进制后去对应的`base64`表中查找对应的值即可

![img](https://img-blog.csdn.net/20180313131013494?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjA1NDUzNjc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

为什么图片转为`base64`后变大了？
因为在进行字符转为后，需要先转为`2`进制，然后再按`6`位划分，划分后前面需要补`2`个`0`，所以也就导致了总字节数变长了。