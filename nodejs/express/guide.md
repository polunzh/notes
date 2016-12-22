# 指南

## 路由
Express支持的路由方法：
> get, post, put, head, delete, options, trace, copy, lock, mkcol, move, purge,
> propfind, proppatch, unlock, report, mkactivity, checkout, merge, m-search,
> notify, subscribe, unsubscribe, patch, search, connect

如果路由方法是非法的JavaScript变量名，可以使用中括号的方法，如：
```
app['m-search']('/', function() {})
```

- `all()`
不是一个http方法，而是加载某一个路径中的中间件：
``` javascript
app.all('/select', function(req, res, next) {})
```
- 路由地址
路由地址可以是字符串， 字符串模式(string patterns)，以及正则表达式

*`query string`不属于`route path`*

由于连字符(-)和点(.)在路由中被翻译为字面意思(interpreted iterally)，所以可以做一些有趣的事情：
``` javascript
路由: /flights/:from-:to
url: /flights/beijing-shanghai

路由: /plantae/:genus.specs
url: /plantae/Prunus/persica
```
- app.route()
路由处理链，如：
``` javascript
app.route('/book')
    .get(function(req, res) {})
    .post(function(req, res) {})
    .put(function(req, res) {})
```

- express.Router
创建模块化的、可mount的路由处理器

## 中间件(middleware)

中间件函数能够访问到req,res，以及应用程序的请求/相应循环中的下一个中间件函数，下一个中间件函数通常
由名为`next`的变量来表示

- 中间件函数可以执行以下任务：
    -　执行任意代码
    - 改变请求／响应对象
    - 结束请求／响应周期
    - 调用堆栈中的下一个中间件

> If the current middleware function does not end the request-response cycle, it must call next() to pass control to 
the next middleware function. Otherwise, the request will be left hanging.

- 中间件的加载顺序是很重要的，先加载的中间件先执行。
- Express应用可以使用下面四种中间件
    - Application中间件
    - 路由中间件
    - 错误处理中间件
    - 内置中间件
    - 第三方中间件

- 如果要跳过路由器中间件堆中的路由，可以使用`next(route)`将控制权转移给下一个路由。
    > `next(route)`仅在使用app.METHOD或router.METHOD函数装入的中间件函数中有效。
### Application中间件
> 使用`app.use()`和`app.METHOD()`函数绑定到应用程序对象的实例
### 路由中间件
> 和Application中间件的工作方式基本相同，只是是用express.Router()的实例来完成的，`router.use()`和`router.METHOD()`
### 错误处理中间件
> 错误处理中间件必须是4个参数：`err, req, res, next`，缺一不可，否则无法进行错误处理。
### 内置中间件
从4.X开始，`Express`不再依赖`connect`中间件，`express.static`是唯一的中间件，该中间件依赖于
[serve-static](https://github.com/expressjs/serve-static?_ga=1.2156208.1809675876.1481434281)。
``` javascript
express.static(root, [options])
```
> You can have more than one static directory per app
``` javascript
app.use(express.static('public'))
app.use(express.static('uploads'))
app.use(express.static('files'))
```
### Third-party middleware
> Use third-party middleware to add functionality to Express app.

## 错误处理
> If you pass anything to the next() function (except the string 'route'), 
    Express regards the current request as being in error and will skip any
    remaining non-error handling routing and middleware functions. If you want
    to handle that error in some way, you’ll have to create an error-handling
    route as described in the next section.
<!-->
> Calls to next() and next(err) indicate that the current handler is complete and
    in what state. next(err) will skip all remaining handlers in the chain except
    for those that are set up to handle errors as described above.

### 默认错误处理程序
如果在开始写`response`后调用`next()`，Express的默认错误处理程序会关掉链接，并且使请求失败。

因此，在添加自定义错误处理序时，如果`header`已经发送到客户端，你可能会想让Express中的默认的
错误处理程序代理：
``` javascript
function errorHandler (err, req, res, next) {
    if (res.headerSent) return next(err)

    res.status(500)
    res.render('error', { error err })
}
```

## Debuging
Express内部使用[debug](https://www.npmjs.com/package/debug)模块记录日志，
debugging默认是关闭的，可以使用DEBUG环境变量打开：
``` javascript
DEBUG=express:*node idnex
```
*Windows*
``` javascript
set DEBUG=express:* & node index
```

使用`express`命令生成的项目使用项目名称作为`namespace`：
```javascript
$ DEBUG={projectname} node ./bin/www
```