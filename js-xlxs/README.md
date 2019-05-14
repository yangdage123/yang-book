# js-xlxs
> 读取excel文件的插件

## 安装

node 中通过npm安装
````bash
	npm install xlxs
````
浏览器使用：
````html
	<script lang="javascript" src="dist/xlsx.core.min.js"></script>
````

## 内部对象
*	workbook	指的是整个 Excel 的文档
*	worksheet	指的是 Excel 中的表
*	cell	指的是 worksheet 中的单元格

大致结构如下：
````js
	// workbook
	{
		SheetsNames: ['sheet1', 'sheet2'],
		Sheets: {
			// worksheet
			'sheet1': {
				// cell
				'A1': {
					t: 's', // 单元格类型(具体类型请看下方的表格)
					v: 'Afghanistan', // 源数据(未经处理的数据)
					r: '<t>Afghanistan</t>', // 解码后的富文本(如果可以被解码)
					h: 'Afghanistan', // 	渲染成HTML格式的富文本(如果可以被解码)
					w: 'Afghanistan', // 格式化后的文本(如果能够被格式化)
					c: '', // 	单元格注释
				},
				'A2': {},
				...
			},
			// worksheet
			'sheet2': {
				// cell
				'A1': {},
				'A2': {},
				...
			}
		}
	}
````
## 用法

1.	用	XLSX.read	读取获取到的 Excel 数据，返回workbook
2.	用	XLSX.readFIle	打开 Excel 文件，返回workbook
3.	workbook.SheetNames	来获取表名
4.	workbook.sheets[表名]	通过表名获取相应的 worksheet
5.	worksheet[address]	通过地址来操作单元格
6.	用	XLSX.utills.sheet_to_json	将单个表获取的数据转成json格式
7.	用	XLSX.writeFile(wb, 'outputFile.xlxs')	生成的新的	Excel	文件

show code

````js
	const XLSX = require(xlxs'');
	// 读取 target/测试.xlxs 文件，得到 workbook 对象
	const workbook = XLSX.readFile('target/测试.xlxs');
	// 获取 workbook 的第一个表名
	const sheetName = workbook.SheetNames[0];
	// 获取 workbook 第一个表的数据
	const worksheet = workbook[sheetName];
	// 打印表格的 A1 位置的数据
	console.log(worksheet['A1'].v);
````

## 最后
>	这个是由于同事需要一份国家中英文的数据，然后后台找了个xlxs，我建议转成json格式。然后，自己动手丰衣足食。感谢万能的互联网提供的资料。

*	参照1：[Node读写Excel文件探究实践](https://aotu.io/notes/2016/04/07/node-excel/index.html)
*	参照2：[js-xlsx模块学习指南](https://segmentfault.com/a/1190000018077543)
