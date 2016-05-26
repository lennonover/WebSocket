# WebSocket
[Node.js|Express|socket.io]
####运行以下命令安装Express
>npm install express-generator -g
####创建项目
>express WebSocket
####进入项目安装npm包
>cd WebSocket 
>npm install
####安装 socket.io
>npm install socket.io
####记得将socket.io加入package.json的dependencies
``` python 
"dependencies": {
    "body-parser": "~1.13.2",
    "cookie-parser": "~1.3.5",
    "debug": "~2.2.0",
    "express": "~4.13.1",
    "jade": "~1.11.0",
    "morgan": "~1.6.1",
    "serve-favicon": "~2.3.0",
    "socket.io": "~1.4.6"
  }
```
####在根目录新建服务端chat_server.js
``` python 
var io = require('socket.io')();
io.on('connection', function (_socket) {
    console.log(_socket.id + ': 已连接');
    _socket.on('message', function (msg) {
        console.log('Message Received: ', msg);
        _socket.broadcast.emit('message', msg);
    });
});

exports.listen = function (_server) {
    return io.listen(_server);
};
```
####修改bin/www文件
``` python 
//var server = http.createServer(app);

/**
 * Listen on provided port, on all network interfaces.
 */

//server.listen(port);
//server.on('error', onError);
//server.on('listening', onListening);

/**
 * Normalize a port into a number, string, or false.
 */
var server = app.listen(app.get('port'), function() {
  console.log('Express server listening on port ' + server.address().port);
});

require('../chat_server').listen(server);
```
####express使用的是jade模板引擎，修改view/layout.jade和view/index.jade 
####启动
>npm satrt



