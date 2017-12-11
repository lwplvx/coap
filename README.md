coap 学习笔记

目前参考 https://segmentfault.com/a/1190000002511350#articleHeader7

目前进行到了 CoAP 数据库查询（代码还没有完全跑通）
代码丢了，下次先补上（hello word 代码已经添加）

Markdown 语法说明 (简体中文版)
http://wowubuntu.com/markdown/#code

## Node CoAP CLI
安装命令如下

     npm install coap-cli -g

 用coap://vs0.inf.ethz.ch/来作一个简单的测试
 
    luweipingdeMac:coap luweiping$ coap get coap://vs0.inf.ethz.ch
    (2.05)	************************************************************
    CoAP RFC 7252                              Cf 1.1.0-SNAPSHOT
    ************************************************************
    This server is using the Eclipse Californium (Cf) CoAP framework
    published under EPL+EDL: http://www.eclipse.org/californium/

    (c) 2014, 2015, 2016 Institute for Pervasive Computing, ETH Zurich and others
    ************************************************************
    luweipingdeMac:coap luweiping$`

 # CoAP Hello,World

 接着我们便开始试试做一个简单的CoAP协议的应用:

 这里用到的是一个Nodejs的扩展Node-CoAP

 `node-coap is a client and server library for CoAP modelled after the http module.`


Node-CoAP是一个客户端和服务端的库用于CoAP的模块建模。创建一个package.json文件，添加这个库

    {
      "dependencies":{
        "coap": "0.7.2"
      }
    }

接着执行

`    npm install`

接着，创建这样一个app.js

    const coap        = require('coap')
        , server  = coap.createServer()

    server.on('request', function(req, res) {
      res.end('Hello ' + req.url.split('/')[1] + '\n')
    })

    server.listen(function() {
      console.log('server started')
    })  

执行

`    node app.js`

便可以在浏览器上访问了，因为现在什么也没有，所以什么也不会返回。

接着下来再创建一个client端的js，并运行之

    const coap  = require('coap') 
        , req   = coap.request('coap://localhost/World')

    req.on('response', function(res) {
      res.pipe(process.stdout)
    })

    req.end()

就可以在console上输出

`    Hello World`

也就达到了我们的目的，用CoAP协议创建一个服务，接着我们应该用它创建更多的东西，如产生JSON数据，以及RESTful。和HTTP版的最小物联网系统一样，CoAP版的最小物联网系统也是要返回JSON的。

# CoAP 数据库查询
## 待续……