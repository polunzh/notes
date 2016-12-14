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