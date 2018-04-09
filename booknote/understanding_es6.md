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

## 函数

### ECMAScript 6 中的默认参数值

在已经指定默认值的参数后可以继续声明无默认值参数，这个时候，只有当不为第二个参数传入值或主动为第二个参数传入`undefined`时才会使用默认值:

```javascript
function foo(url, timeout = 2000, callback) {}

foo('/sources', undefined); // 使用默认值
foo('/sources'); // 使用默认值
foo('/sources', null); // null 是有效值，不会使用默认值
```

### 默认参数值对 arguments 对象的影响

`ES6`中的严格模式下，arguments 对象不再随着函数参数的变化而变化:

```javascript
function minxArgs(first, second) {
  'use strict';

  console.log(arguments[0] === first); // true
  console.log(arguments[1] === second); // true
  first = '1';
  second = '2';
  console.log(arguments[0] === first); // false
  console.log(arguments[1] === second); // false
}

minxArgs(3, 4);
```

#### 参数的 TDZ

```javascript
function add(first = second, second) {
  return first + second;
}

add(1, 1);
add(undefined, 1);
```

函数参数有自己的作用域和临时死区，其与函数体的作用域是独立的，也就是说函数参数的默认值不可以访问函数体内声明的变量。

### 不定参数

#### length属性

函数的`length`属性统计的是函数命名参数的数量，不定参数不会影响`length`的值:

``` javascript
function foo(a, ...keys) {} // foo.length=1
function foo(b, b, ...keys) {} // foo.length=2
```

#### 限制

1. 每个函数只能声明一个不定参数
1. 不定参数必须放到所有参数的末尾
1. 不定参数不能用于对象字面量的`setter`参数中, 因为`setter`只能有一个参数，但是不定参数可以有多个

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
