# AMD & CMD & CommonJS

## 分类
- 同步：CommonJS
- 异步：AMD & CMD

同步CommonJS适用于node.js，在服务器端，资源不需要网络传输，同步加载即可。

## AMD
在浏览器环境中，所有资源需要通过网络加载，使用同步加载会使程序阻塞。AMD采用==异步加载==模块依赖，在回调中执行模块代码，不影响其他代码执行。

	define(id?, dependencies?, factory);  

> RequireJS执行流程：  
	1. require函数检查依赖的模块，根据配置文件，获取js文件的实际路径  
	2. 根据js文件实际路径，在dom中插入script节点，并绑定onload事件来获取该模块加载完成的通知  
	3. 依赖script全部加载完成后，调用回调函数  


## CMD
不需要在定义的时候写明依赖的组件，在需要的地方用require的方式引入依赖。  

	define(function(require,exports,module){...});


> SeaJS执行流程：  
	1. 通过回调函数的Function.toString函数，使用正则表达式来捕捉内部的require字段，找到require('jquery')内部依赖的模块jquery  
	2. 根据配置文件，找到jquery的js文件的实际路径  
	3. 在dom中插入script标签，载入模块指定的js，绑定加载完成的事件，使得加载完成后将js文件绑定到require模块指定的id（这里就是jquery这个字符串）上  
	4. 回调函数内部依赖的js全部加载（暂不调用）完后，调用回调函数  
	5.  当回调函数调用require('jquery')，即执行绑在'jquery'这个id上的js文件，即刻执行，并将返回值传给var b


## CommonJS
CommonJS定义的模块分为  
- `require`  模块引用   
- `exports` 模块定义  
- `module`  模块标识  












