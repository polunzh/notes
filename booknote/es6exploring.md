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
const [, year, month, day] = /^(\d\d\d\d)-(\d\d)-(\d\d)$/.exec('2019-12-21');
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
class MyError extends Error {}
```

15. 使用内置的Map数据结构

``` javascript
const map = new Map();
function countWords(word) {
    const count = map[word] || 0;
    map.set(word, count + 1);
}
```

ES5:
``` javascript
var dict = Object.create(null);
function countWords(word) {
    var escapeKey = escapeKey(word);
    if(escapeKey in dict) {
        dict[escapeKey]++;
    } else {
        dict[escapeKey] = 1;
    }
}

function escapeKey(key) {
    if(key.indexOf('__proto__') === 0) {
        return key + '%';
    } else {
        return key;
    }
}
```

*而且Map的key可以不是字符串*

16. 新的字符串方法
    - startsWith()

    ``` javascript
    str.indexOf(s) === 0; // ES5
    str.startsWith(s); // ES6
    ```
    - endsWith()
    - includes()
    ``` javascript
    str.indexOf('s') >=0; // ES5
    str.includes('s'); // ES6
    ```

    - repeat()
    ``` javascript
    new Array(3+1).join('#'); // ES5, hack
    '#'.repeat(3); // ES6
    ```

17. 新的数组方法
    - Array.prototype.indexOf -> Array.prototype.findIndex
    ``` javascript
    const arr = [1, NaN];

    arr.indexOf(NaN); // -1
    arr.findIndex( x=> Number.isNan(x))); // 1
    ```

    * Number.isNaN() 是比 isNaN() 更安全的方法，因为isNaN会强制转型*
    ``` javascript
    isNaN('a'); // true
    Number.isNaN('a'); // false
    ```

    - Array.prototype.slice() -> Array.from(),或者使用展开操作符(`...`)
    
    > 在ES5中，`Array.prototype.slice`方法用来将类数组对象转换为数组;
    > 如果一个值是可迭代的，也可以使用展开操作符来转换

    ``` javascript
    var arr1 = Array.prototype.slice.call(arguments); // ES5
    const arr2 = Array.from(arguments)
    const arr3 = [...arguments]
    ```
    
    - apply() -> Array.fill()

    > 在`ES5`中可以是用`apply`的`hack`方式来创建任意长度的`undefined`数组

    ES5:
    ``` javascript
    Array.apply(undefined, new Array(2));
    ```

    ES5:
    ``` javascript
    new Array(2).fill(undefined)
    ```

- CommonJS modules -> ES6 modules
 
``` javascript
import * from 'lib'
```

Single exports
``` javascript
export default function() {}
```

## Modules

1. Single export

导出默认匿名对象不需要分号
``` javascript
export default function() {} // 没有分号
export default class {...} // 没有分号
```

2. `Modules`是单例

即使被导入多次，只有一个实例存在

3. ECMAScript 5 modules systems

    - CommonJS Modules

    > 主导该规范实现的是NodeJS

        *特点*
        - 紧凑语法(Compact syntax)
        - 服务器端同步加载
    - Asynchronous Module Definition(AMD)

    > `RequireJS`是该规范最流行的实现
    
        *特点*
        -  稍比较复杂的语法，在适使用`eval()`的情况下使`AMD`工作
        - 为服务器端和浏览器端异步加载设计

4. ECMAScript 6 modules

> 两种导出方法：命名导出（一个模块可以导出多个），`default exports`（每个模块导出一个），
> 可以混用，但是尽量分开。

