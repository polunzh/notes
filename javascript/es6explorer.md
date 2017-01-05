## Core ES6 feature

1. var to let/const
> 优先使用`const`, 只要值不再改变的变量就用`const`；否则用`let`；避免用`var`。

2. IIFEs to blocks

如果在ES5中想限制变量在一个块作用域中，你需要使用一个叫做IIFE(Immediately-Invoked Function Expression)的模式：
``` javascript
(function(){
    var tmp...
}());
```

在ES6中只需要使用一个块声明或者一个const声明就行了：

``` javascript
{
    let tmp = ...
}
```

3. 字符串插值

避免字符串拼接, 以及多行字符串。

4. 函数表达式 to 箭头函数

``` javascript
function UiComponent() {
    var button = document.getElementById('mybutton');
    button.on('click', ()=>{
        console.log('CLICK');
        this.handleClick(); //  这里的this是UiComponent的this，还不知道为什么
    });
}
```

5. 处理多个返回值

使用数组返回多个值
``` javascript
const [, year, month, day] = /^(\d\d\d\d)-(\d\d)-(\d\d)$/.exec('2019-12-21);
```
> 上面例子中数组的第一个逗号是为了跳过数组第一个元素，因为`/^(\d\d\d\d)-(\d\d)-(\d\d)$/.exec('2019-12-21')`
返回的是`["2019-12-21", "2019", "12", "21"]`

使用`objects`返回多个值
> 所谓的解构`Destructuring`
``` javascript
const {writable, configurable} = Object.getOwnPropertyDescriptor(foo, 'foo')
```

6. 使用`for-of`替换`for`和`forEach`
> `for`循环的优势是可以被中断(break)，`forEach`简洁, 而`for-of`兼顾了`for`,`forEach`的优点

如果同时需要索引和值，可以使用`Array`的`entries`:

``` javascript
for(const [index, elem] of arr.entries()) {
    console.log(`${index}, ${elem}`);
}
```

7. 使用参数默认值
> ES6中只有`undefined`才能触发默认值

8. 命名参数

通过字面对象实现（所谓的`可选对象模式`）
``` javascript
function selectEntries( { start=0, end=1, step=1 }) {}
```

9. 剩余参数(Rest Parameters)
> 使用`...`操作符实现
``` javascript
function logAllArguments(...args) {
    for (const arg of args) {
        console.log('---');
        console.log(arg);
    }
}
```

可选参数:
``` javascript
function selectEntries({ start=0, end=-1, step=1 } = {}) {
    ···
}
```

10. 展开操作符`...`替换`apply()`

> 在ES5中，将数组转换为参数使用`apply()`, ES6中可以使用`...`
``` javascript
Math.max(...[1, 21, 2, -10])

let arr1 = ['a', 'b'];
const arr2 = ['c', 'd'];

arr1.push.apply(arr1, arr2); // arr1=['a', 'b', 'c', 'd'] ES5
arr1.push(...arr2); // arr1=['a', 'b', 'c', 'd'] ES6
```

11. 展开操作符`...`替换`concat()`

``` javascript
const ar1 = ['a', 'b'];
const ar2 = ['c'];
const ar3 = ['d'];
console.log([...ar1, ...ar2, ...ar3]);
```

12. 在字面对象中，用定义方法的方式替换函数表达式

13. 类替换构造函数(From constructors to classes)

Base classes
``` javascript
    class Person {
        constructor(name) {
            this.name = name;
        }

        describe() {
            return 'Person called' + this.name;
        }
    }
```
Derived classes
``` javascript
    class Employee extends Person {
        constructor(name, title) {
            super(name);
            this.title = title;
        }

        describe() {
            return super.describe() + '(' + this.title + ')';
        }
    }
```

14. 使用继承`Error`类的方式的替换`自定义error构造函数`

``` javascript
class MyError extends Error {

}
```