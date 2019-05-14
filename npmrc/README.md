# .npmrc文件
> npm的配置文件，我们可以通过**npm config**命令来更新全局的npmrc文件内容

npm的配置的文件都是 **key = value** 格式的参数列表。
```
	registry = https://registry.taobao.org/
```

可以使用环境变量 **${VARIABLE_NAME}**。
```
	prefix = ${HOME}/.npm-package
```

可以通过在键名后面加"[]"来指定数组值。
```
	key[] = "first value"
	key[] = "second value"
```

使用**#**或者**;**开头来注释。
```
	# 这是测试
	; 这是测试
```

## 每个项目的配置
在项目本地本地工作时，**.npmrc**文件放在项目的根目录，他将设置此项目的配置值。

**注意**这仅适用正在运行的项目。在发布模块时，它不起作用。例如，您无法发布强制自身全局安装或在其他位置安装的模块。
而且，不会在全局模式下读取，例如运行`npm install -g`时。

## registry
> 设置仓库地址

### 参考
部分例子是直接copy的官方的文档，另外，感谢Google翻译！！！
* [npmrc文档](https://docs.npmjs.com/files/npmrc)
* [npm-config文档](https://docs.npmjs.com/misc/config)
