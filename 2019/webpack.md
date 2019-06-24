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