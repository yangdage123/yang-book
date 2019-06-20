# js

## 浏览器标签页切换
> 浏览一个网站的时候发现浏览器标签页切换的时候，页面的title发生了变化

主要是监听了`document`的`visibilitychange`事件来做到的，然后通过判断`document.hidden`来判断当前是在别的标签页还是在当前标签页。

````js
	// 主要是处理兼容性 如果 分别判断 hidden、webkitHidden、mozHidden
	const hidden ='hidden' in document ? 'hidden' : 'webkitHidden' in document ? : 'webkitHidden' : 'mozHidden' in document ? 'mozHidden' : null;
	// 如果hidden 是 null的话表示不支持
	if (hidden) {
		const visibilityChangeEv = hidden.replace(/hidden/i, 'visibilitychange');
		document.addEventListener = () => {
			if (!document[hidden]) {
				console.log('页面非激活状态');
			} else {
				console.log('页面激活状态');
			}
		}
	}
````
代码参考：
	[关于浏览器标签页间切换触发的事件的理解](https://segmentfault.com/q/1010000010305827)
资料参考：
	[JS 监听浏览器各个标签间的切换](https://www.yduba.com/qianduan-1491588986.html)
实现参考：
	[knex.js中文文档-查询](https://www.songxingguo.com/2018/06/30/knex.js-query/)


## 在输入框内进行光标的移动
> 在onfocus的时候移动`selectionStart`和`selectionEnd`

```
	function onFocus (e) {
		// 获取触发事件的DOM
		const el = e.target;
		const len = el.value.length;
		if (typeof el.seletionStart === 'number' && typeof el.seletionEnd === 'number) {
			// 平时所见的光标其实是由两部分组成的，即selectionStart和selectionEnd，一般时候这两个是相等的
			// 但在选中一段文字，全选时，他们的差值就是所选文字的个数
			el.selectionStart = len;
			el.selectionEnd = len;
		}
	}
```
copy自[csdn](https://blog.csdn.net/m0_37582289/article/details/78968251)