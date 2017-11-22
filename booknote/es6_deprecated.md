# ES6 学习笔记

> 学习自[阮一峰的es6教程](http://es6.ruanyifeng.com/)
> 2016年11月20日10:47:26

## let 和 const
### let
1. 只在声明的代码块中有效
2. 不存在变量提升，所以必须先声明后使用
3. `暂时性死区`: 只要一进入当前作用域,所使用的变量就已经存在了，只是不可以取,只有等到声明变量的
    那一行出现,才可以使用和获取该变量
4. 不允许重复声明变量
5. 在块级作用域中可以声明函数（es5的严格模式下会报错）,不过对于浏览器中的es6不遵守该规则；而且
    只在使用大括号的情况下成立：

    ``` javascript
    'use script'
    if(true) {
        function f() {}
    }

    // 报错
    'use script'
    if (true)
        function f() {}
    ```
### const
1. const命令只是保证变量名指向的地址不变，并不保证该地址的数据不变；如果想将对象冻结,应该使用
    Object.freeze()方法
2. es6中声明变量的方法: var, function, let, const, import和class

> 优先使用`const`, 只要值不再改变的变量就用`const`；否则用`let`；避免用`var`;


## 顶层对象的属性
    var 和 function声明的全局对象仍然是顶层对象的属性;但是另一方面，let、class和const声明的
    全局变量不再属于顶层对象的属性。

## 顶层对象
    在es5中顶层对象在浏览器和Node等环境下不太一致，在es5中:
- 浏览器里面，顶层对象是window，但Node和Web Worker没有window。
- 浏览器和Web Worker里面，self也指向顶层对象，但是Node没有self。
- Node里面，顶层对象是global，但其他环境都不支持。

> `system.global`模拟了在所有环境下把`global`作为顶层对象

## 变量的解构赋值
> `es6`允许按照一定模式，从数组和对象中提取值,对变量进行赋值,这一过程称为`解构(Destructuring)`

- 如果等号右边不是可遍历的结构，那么将会报错
- 结构中允许指定默认值：let [ foo = true ] = [],需要注意的是es6中使用严格相等(===)
    来确定一个位置是否有值:
    ``` javascript
    let [foo = 1] = [undefined] // foo = 1
    let [foo = 1] = [null] // foo = null
    ```
- 解构赋值的规则是，只要等号右边的值不是对象，就先将其转换为对象。