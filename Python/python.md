# Python学习笔记

## 基本概念

### 字面量
> 一个字面意义上的常量的例子是如同5、1.23、9.25e-3这样的数，或者如同'This is a string'、"It's a string!"这样的字符串。
> 它们被称作字面意义上的，因为它们具备 字面 的意义——你按照它们的字面意义使用它们的值。数2总是代表它自己，
> 而不会是别的什么东西——它是一个常量，因为不能改变它的值。因此，所有这些都被称为字面意义上的常量

## 数
> Python中有4种类型的数--整数/长整数/浮点数和复数

## 字符串
- 单引号`'`和双引号`"`是完全相同的
- 三引号`'''`或`"""`表示多行字符串
- 自然字符串：如果你想要指示某些不需要如转义符那样的特别处理的字符串，那么你需要指定一个自然字符串。自然字符串通过给字符串加上前缀r
    或R来指定。例如r"Newlines are indicated by \n"。
- Unicode字符串：在字符串前加`U`或`u`
- 字符串是不可更改的
- 按字面意义级连接字符串：如果把两个字符串按字面意义相邻放着，他们会被Python自动连接。eg,'What is ' 'your name'

## 面向对象
> 就每一个东西包括数/字符串甚至函数都是面向对象的这一点来说，Python是完全面向对象的。

### 逻辑行和物理行
- 默认地，Python希望每行都只使用一个语句，这样使得代码更加易读。
- 如果你想要在一个物理行中使用多于一个逻辑行，那么你需要使用分号（;）来特别地标明这种用法。分号表示一个逻辑行/语句的结束。
- `但是强烈建议每个物理行只有一个逻辑行`

## 控制流
while,for in等循环都可以用else语句（`以前没有注意到`)，除非使用了`break`,否则`else`一定会执行:
``` python

    # for in
    for i in range(1,5):
        print i
    else:
        print 'The for loop is over.'


    # while
    while running:
        guess = int(raw_input('输入一个数字：'))

        if guess == num:
            print 'bingoo!'
            running = False
        elif guess > num:
            print '大了'
        else:
            print '小了'
    else:
        print '循环完了'
    print 'Done!'
```

## 函数

### `global`,定义全局变量

### 参数
- `默认参数`放在最后
- '关键字参数'，通过命名来为参数赋值

### `return`语句
- 没有返回值的`return`语句等于`return None`
- 除非提供了`return`语句，否则每个函数都在结尾默认暗含`return`

### 文档字符串`DocStrings`
> 在函数第一个逻辑行的字符串是这个函数的`文档字符串`

## 模块`module`

- 尽量避免使用`from modulename import *` 语句，这样可以提高程序的可读性
- `__name__`,每个Python模块都有它的`__name__`，如果它是`__main_`，这说明这个模块被用户单独运行，我们可以进行相应的恰当操作。

## 数据结构
- 使用`items()`遍历字典中的`key/value`
- 使用`in`/dict.has_key()检查一个key是否存在
