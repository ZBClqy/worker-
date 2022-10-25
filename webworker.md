# WebWorker

webWorker就是用来解决js单线程，就是异步但是遇到大的模块需要加载运算时也很慢，h5就为我们提供了webWorker让我们的js脚本在后台进行多线程般的操作。不过目前低版本的浏览器还无法兼容。

## 一、HTML页面示例

<body>

​	woker脚本监听内容<span id="msg"></span>

​	<input type="text" id="app"/>

<button onclick="setMessage()">发送</button>

<button onclick="stopWorker()" >停止</button>	

</body>

## 二、js页面示例

if ( typeof(Worker) ==="undefine" ) {	//检查是否存在Worker

​		console.log("当前浏览器不兼容Worker") //不存在发出提醒

}else{

​		let w=new Worker('worker.js')

​		w.onerror=(error)=>{

​				console.log("出错了")  	//如果报错执行到这

​				w.terminate()

​		}

​		w.onmessage=(ev)=>{	//这里监听worker返回回来的信息

​				document.querySelector("#msg").innerHtml=ev.data		

​		}

​		function setMessage(){ 	

​				let app=document.querySelector("#app")

​				w.postMessage(app.value) 	//这里将我们的dom的value发送给worker

​		}

​		function stopWorker(){

​				w.terminate()	//这里关闭我们的worker

​		}	

}

## 三、worker.js示例

​	onmessage=(ev)=>{	//这里监听我们的js发送过来的数据

​		postMessage(ev.data+"787878") 	//这里将我们worker中的内容发送回我们的js

}