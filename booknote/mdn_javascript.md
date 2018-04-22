# ECMA JavaScript

## 基础知识

### Function.prototype.apply

> [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply):
> The `apply()` method calls a function with a given `this` value, and `arguments` provided as an array(or an `array-like object`)

```javascript
`Example`;
const numbers = [2, 1, 10];
const max = Math.max.apply(null, numbers); // === Math.max(...numbers) = 2
const min = Math.min.apply(null, numbers); // === Math.min(...numbers) = 1
```

### Function.prototype.bind

`bind()`方法创建一个新的函数，当被调用时，将其`this`关键字设置为提供的值，在调用新函数时，在任何参数提供之前提供一个给定的参数序列。

`bind()` 函数会创建一个新函数（绑定函数），新函数与被调用函数具有相同的函数体（`ES5`中的`call`属性）。当新函数被调用时`this`值绑定到`bind()`的第一个参数，该参数不能被重写。绑定函数被调用时，`bind()`也接受预设的参数提供给原函数。一个绑定函数也能使用`new`操作符创建对象，但是这是`this`的值会被忽略。

#### 返回值

返回由指定`this`值和初始化参数改造的拷贝函数。

`偏函数`

## 原型链
