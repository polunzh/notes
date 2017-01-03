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

- app.param([name], callback)

- app.use([path], callback[,callback ...])

    - 加载指定的中间件函数，或者加载中间件到指定的path：中间件函数在请求的根路径匹配到的时候执行。
    - `path`的默认值是`/`,如果中间件函数没有被mounted到任何一个路径上，那么默认是`/`, 即：每次都会被执行。
    - 中间件是按顺序执行的，所以中间件的顺序是很重要的:
    ``` javascript
    // 截获或有请求并返回
    app.use(function(req, res, next){
        res.send('hello word0');
    });


    // 改路径不会被执行
    app.use('/', function (req, res, next) {
        res.send('hello word0');
    });
    ```
## Request

- `req.get`等同于`req.header`
- req.is(type)

用`type`去匹配request的`Content-Type`的`HTTP`头部，如果相匹配，返回`true`
- `req.param`已弃用

## Response
- `res.cookie(name, value, [, options])`
    - `option.encode`不支持异步函数
    - `option.maxAge`：设置`expries`为最近n毫秒的方便选项

- `res.json`

> 发送一个JSON响应，该方法将参数转换为JSON字符串；该方法用`JSON.stringify`方法转换为JSON字符串

- `res.location(path)`

`path`如果是`back`,有特殊含义，是指`request`的`referer`头部属性

- `res.redirect`

    - 参数`back`有特殊含义，指`request`的`referer`头部
    - `..`，跳转到上一级路径， 如,
        > 当前路径，`http://example.com/admin/post/new`，`res.redirect('..')`跳转到`http://example.com/admin/post`

- `res.render(view, [,locales][,callback]`

    - `locales.cache`在`production`环境中默认为`true`
    - `callback`，返回渲染错误（如果有）和渲染完成的字符串，但是不会做出相应
    - 如果渲染失败，`res.render`内部会调用`res.next(err)`

- `res.send([body])`

> `body`参数可以是一个`Buffer`对象，字符串，`object`或者数组

- `res.sendStatus(statusCode)`

> 设置相应状态码，而且返回其相应的字符串表示形式，如：

``` javascript
res.sendStatus(200); // 等于res.status(200).send('OK')
res.sendStatus(403); // 等于res.status(403).send('Forbidden')
```

- res.set(field[, value])

    - 等同于`res.header(field[,value])`
    - 如果要同时设置多个值，可以传一个对象：
    ``` javascript
    res.set({
        'Content-Type': 'application/json',
        'Content-Length': '123',
        'ETag': '12345'
    })
    ```

- res.type(type)

设置`Content-Type`的MIME类型，由[mime.lookup](https://github.com/broofa/node-mime?&_ga=1.104008192.1809675876.1481434281#mimelookuppath)
指定，如果`type`包含`/`，则直接设置为`Content-Type`的值：

``` javascript
res.type('.html') => 'text/html'
res.type('html') => 'text/html'
res.type('json') => 'application/json'
res.type('application/json') => 'application/json'
```

## Router

- router.param(name, callback)