# webpack
> webpack的基本配置

## entry

````js
	module.exports = {
		entry: {
			index: './src/entry.jsx',
			vendor: [
				// 一般把第三方库作为单独打包，会出现vendor的文件
			]
		}
	}
````

## output

output.path
output.filename
output.chunkFileName
output.publicPath

````js
	module.exports = {
		output: {
			path: path.resolve(__dirname, 'dist'), // 打包的输出路径
			filename: '[name].[chunkhash].js', // 打包输出的文件名
			chunkFileName: '[name].[chunkhash].js', // 打包输出未列在entry中的文件
			publicPath: 'dist/', // 运行的时候文件路径
		}
	}
````

## cache
> 缓存生成的 webpack 模块和 chunk，来改善构建速度

## resolve

resolve.alias
````js
	// webpack
	module.exports = {
		resolve: {
			alias: {
				lib: path.resolve(__dirname, 'src/lib'), // 这样直接import
			}
		}
	}
	// js 文件
	import * from 'lib';
````

resolve.extensions
````js
	// webpack
	module.exports = {
		resolve: {
			extensions: ['js', 'json', 'css', 'jsx']
		}
	}
	
	// js文件 引入文件的时候不需要扩展名
	import * from 'lib/test' // import * from 'lib/test.js'
````

resolve.externals

从cdn中引入jquery
````html
<script
  src="https://code.jquery.com/jquery-3.1.0.js"
  integrity="sha256-slogkvB1K3VOkzAI8QITxV3VzpOnkeNVsKvtkYLMjfk="
  crossorigin="anonymous">
</script>
````

````js
	// webpack
	module.exports = {
		externals: {
			jquery: 'jQuery',
		}
	}
	
	// 可以直接使用而不会报错
	import $ from 'jquery';
	
	$('div').css(/* ... */)
````
## module

## webpack.DefinePlugin
> 创建一个在编译的时候的环境变量

````js
	module.exports = {
		plugins: [
			new webpack.DefinePlugin({
				TEST: JSON.stringify('test')
			})
		]
	}
````

## extract-text-webpack-plugin
> 打包项目中所有css

````js
	const ExtractTextPlugin = require('extract-test-webpack-plugin');
	
	module.exports = {
		module: {
			rules: [
				{
					test: /\.css$/,
					use: ExtractTextPlugin({
						fallback: 'style-loader',
						use: ['css-loader', 'sass-loader']
					})
				}
			]
		},
		plugins: [
			new ExtractTextPlugin('[contenthash].css')
		]
	}

````
## webpack-parallel-uglify-plugin
> 代码优化压缩

````js
	const ParallelUglifyPlugin = require('webpack-parallel-uglify-plugin');

	module.exorts = {
		plugins: [
			// 使用 ParallelUglifyPlugin 压缩混淆代码
			new ParallelUglifyPlugin({
				// 传给 UglifyJS 参数
				uglifyJS: {
					output: {
						// 是否输出 可读性较强的代码，默认为true
						beautify: false,
						// 是否输出 注释，默认为true
						comments: false,
					},
					compress: {
						// 是否在UglifyJS删除无用代码的时候输出警告信息，默认为true
						warning: false,
						// 是否删除代码中所有的console语句，默认false
						drop_console: true,
						// 是否折叠变量，例：var x = 1; y = x;转换成 y = 1，默认为false
						collapse_vars: true,
						// 是否提取出现多次但是没被定义成常量引用的值，例：x = 'XXX'; y = 'XXX';转换成 const a = 'XXX'; x = a; y = a;默认为false
						reduce_vars: true,
					}
				}
			})
		]
	}
````

ParallelUglifyPlugin的其他配置参数
属性 | 默认值 | 描述
 --- | --- | --- 
 test | /.js$/ | 使用正则匹配需要被ParallelUglifyPlugin处理的文件
 include | 空 | 使用正则去匹配需要被ParallelUglifyPlugin处理的文件
 exclude | 空 | 使用正则去匹配不需要被ParallelUglifyPlugin处理的文件
 cacheDir | 不缓存 | 缓存处理后的结果，下次遇到一样的输入时直接从缓存中获取处理后的结果并返回，cacheDir 用于配置缓存存放的目录路径。
 workerCount | 当前电脑CPU核数减去1 | 开启几个子进程去并发的执行
 sourceMap | 不生成 | 否为处理后的代码生成对应的Source Map，开启后耗时会大大增加，一般不会将处理后的代码的sourceMap发送给网站用户的浏览器。


