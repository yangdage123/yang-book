# y-logger

> nodejs log的小工具

## 由来
> 在做`webpack-demo`的时候进行start，发现控制台有不同的颜色。所以google了一下，于是一发不可收拾。

在浏览器环境中，可以`console.log('%c hello', 'color: red')`来进行样式修改。
所以在做`webpack-demo`的时候尝试写带颜色的`console`，发现并不可以。

又通过google发现node中控制台显示颜色与浏览器中不一样，所以照着网上的信息来做一个，发现console出来的还挺好看的。

第一个网上找到的资料是使用**\\033**开头的，但是发现在严格模式下不允许八进制，所以使用了**\\u001b**开头。

于是，便想，能不能吧一些基础的**info**、**success**、**warn**、**error**的console封装起来。

基本的大概设想是，暴露四个方法info、success、warn、error，分别console响应的样式。

于是写了一个class，内部包涵四个行数。然后发现console部分的代码基本一致，又写了一个log函数，可以传入type、title和内容。

由于每个函数都支持传入title或者不传入title，所以要对传入参数的长度做判断。

如果传入的参数大于1，我就认为第一个参数是作为title显示的，其他的都是content内容。

于是由写了一个createBaseFun，在调试console error颜色的时候发现黑底+黄色的title还挺好看的，便觉得可以把黑底+颜色文字设置为black的主题。

于是做着做着，基本就ok了。

## 最后
> 感谢互联网提供的资料。

*	[使Node.js中的console.log()输出彩色字体](https://www.jianshu.com/p/cca3e72c3ba7)
*	[Node.js Color 模块实现入门浅析](https://zhuanlan.zhihu.com/p/27308276)
