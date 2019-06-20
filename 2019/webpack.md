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

