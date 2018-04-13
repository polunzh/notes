# ECMA JavaScript

## 基础知识

### Function.prototype.apply

> [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply):
The `apply()` method calls a function with a given `this` value, and `arguments` provided as an array(or an `array-like object`)

``` javascript
`Example`
const numbers = [2, 1, 10];
const max = Math.max.apply(null, numbers); // === Math.max(...numbers) = 2
const min = Math.min.apply(null, numbers); // === Math.min(...numbers) = 1
```

### Function.prototype.bind

 `bind()`方法创建一个新的函数，当被调用时，将其`this`关键字设置为提供的值，在调用新函数时，在任何参数提供之前提供一个给定的参数序列。

 `返回值`
 `偏函数`
