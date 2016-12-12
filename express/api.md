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
