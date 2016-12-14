# API笔记

> 这里只记录之前不知道的

## express()
创建一个Express应用，`express`模块导出的顶级函数。

### 方法
- express.static(root, [options])

    - options.fallthrough
    > When this option is true, client errors such as a bad request or a request to
    > a non-existent file will cause this middleware to simply call next() to invoke
    > the next middleware in the stack. When false, these errors (even 404s), will
    > invoke next(err).

    - setHeaders
    > 函数签名: `fn(res, path, stat)`

- express.Router([options])
创建新的[router](http://expressjs.com/en/4x/api.html#router)对象

options:
| 属性  | 描述  | 默认值  | 可用性 |
|---|---|---|---|
| caseSensitive  |   | false  |
| mergeParams  | Preserve the req.params values from the parent router. If the parent and the child have conflicting param names, the child’s value take precedence.  |   | 4.5+ |
| strict | |	Disabled by default, “/foo” and “/foo/” are treated the same by the router. | |

## Application
由express()函数导出的对象：
``` javascript
app = express()
```

`app`有以下方法：
- HTTP请求路由， 如`app.METHOD`和`app.param`
- 配置中间件：`app.route`
- 渲染模版：`app.render`
- 注册模版引擎：`app.engine`

### app.get(name) 和app.get(path, callback[,callback ...]),

参数不同，方法的含义不同。

### app.listen(path, [callback])

> Starts a UNIX socket and listens for connectiosn on the given path. This method is
> identical to Node's [http.Server.listen()](https://nodejs.org/api/http.html#http_server_listen_path_callback)

### app.listen(port, [hostname],[backlog],[callback])

> Binds and listen for conenctions on the specified host and port. This method is
> identical to Node's [http.Server.listen()](https://nodejs.org/api/http.html#http_server_listen_path_callback)

> The app returned by express() is in fact a JavaScript Function, designed to be
> passed to Node’s HTTP servers as a callback to handle requests. This makes it
> easy to provide both HTTP and HTTPS versions of your app with the same code base,
> as the app does not inherit from these (it is simply a callback):

``` javascript
var express = require('express);
var https = require('https');
var http = require('http');
var app = express();

http.createServer(app).listen(80);
https.createServer(options, app).listen(80);
```
### app.param(name, callback)

- 只用用在注册在app上的路由，而且不能继承，所以不能用于其子项目(sub-app)；而且注册在`app`上的
`express.Router`对象也不行。
- 在一次请求/响应周期中每个参数只触发一次，即使这个参数被匹配到了多次。