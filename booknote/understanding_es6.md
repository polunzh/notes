# 深入理解 ES6

[TOC]

## 块级作用域绑定

### TDZ

_Temporal Dead Zone_

```javascript
// snippet-1: 正常运行
const condition = true;
if (condition) {
  console.log(typeof log);
  var log = 'log';
}

// snippet-2: 正常运行
const condition = true;
console.log(typeof log);
if (condition) {
  let log = 'log';
}

// snippet-3: ReferenceError: log is not defined
const condition = true;
if (condition) {
  console.log(typeof log);
  let log = 'log';
}

// snippet-4
let a = 1;
{
  a = 2;
  let a;
  console.log(a);
}
```

在`ES6`中，`let`也会出现`hoisting`的现象（snippet-4)，但是在`LexicalBinding`之前是无法访问的，这个时候的变量会存在于所谓的`TDZ`中。

### 循环中的 let

```javascript
// snippet-var
var funcs = [];
for (var i = 0; i < 10; i++) {
  funcs.push(function() {
    console.log(i);
  });
}

funcs.forEach(func => {
  func();
});

// 输出 10个10
```

如果使用`let`

```javascript
// snippet-let
var funcs = [];
for (let i = 0; i < 10; i++) {
  funcs.push(function() {
    console.log(i);
  });
}

funcs.forEach(func => {
  func();
});
// 输出 0-9
```

`let`在循环中内部的表现是专门定义的，并不一定和"`let`的不提升"相关。

### 全局块作用域绑定

`var`会覆盖全局变量，但是 `let`和`const`不会，只是会在当前作用域中覆盖。

## Promise

### Promise 链的返回值问题

Promise 链的另一个重要特性是可以给下游 Promise 传递数据。

```javascript
let p1 = new Promise(function(resolve, reject) {
    resolve(42);
});

p1.then({
    console.log(value);    // "42"
    return value + 1;
}).then(function(value){
    console.log(value);   // "43"
});
```

### Promise 链中返回 Promise

```javascript
let p1 = new Promise((resolve, reject) => {
  resolve(42);
});

let p2 = new Promise((resolve, reject) => {
  resolve(43);
});

p1
  .then(value => {
    console.log(value); // "42"
    return p2;
  })
  .then(value => {
    console.log(value); // "43"
  });
```

### Promise.race

接收多个受监视的`Promise`的可迭代对象作为参数，返回可迭代对象中第一个被`resovle`或`reject`的`Promise`对象。

#### 例子

```javascript
const p1 = new Promise((resolve, reject) => setTimeout(resolve, 200, 'p1'));
const p2 = new Promise((resolve, reject) => setTimeout(resolve, 100, 'p2'));
const p3 = new Promise((resolve, reject) => setTimeout(resolve, 200, 'p3'));

const result = Promise.race([p1, p2, p3]);
result.then(content => console.log(content)).catch(error => console.log(error)); // p2
```
