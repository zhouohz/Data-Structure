# 第一章 JavaScript简介

## JS数据结构和算法

## 环境搭建

### 最简单的环境搭建

在html页面中内嵌或引用JS代码。通过浏览器开发工具调试或查看结果

### 使用WEB服务器

使用web服务器，如：XAMPP

### 使用Node搭建WEB服务器

用Node.js搭建web服务器

```shell
sudo npm install http-server -g
```

切换到示例代码的根目录，执行`http-server`，打开所示链接即可

### 直接执行JS代码

安装nodemon检测JS文件的改动，自动重新执行

```shell
sudo npm install nodemon -g

## 使用
nodemon path/foo.js
```

## JS基础

### 变量

JS是弱类型的语言

null表示变量没有值，undefined表示变量已被声明，但尚未赋值

变量的作用域分为：全局作用域和函数作用域

在函数中如果没有使用var关键字声明变量，则为全局变量

### 操作符

算数操作符：+ - * / % ++ --

赋值操作符：= += -= \*= /= %=

比较操作符：== \=== != !== > >= < <=

逻辑操作符：&& || !

位操作符：& | ~ ^ << >>

typeof：返回变量或表达式的类型

delete：删除对象里的属性

### 真值和假值

除了0 NaN "" null undefined为false以外，其余都是true

### 相等操作符（\==和===）

使用`==`时JS会进行隐式转化，其他类型转化为数值类型再进行比较

null -> 0; undefined -> NaN;

String：如果含有字符则转化为NaN，只有数字则转化为对应的数值

Boolean：true -> 1, false -> 0

NaN不与任何值相等，包括它自己

## 控制结构

### 条件语句

if...else

switch...case(内部用的是全等)

三元操作符

### 循环

for

while

do...while(至少执行一次，即使条件不满足)

## 函数

默认返回值为undefined

多余的实参会被忽略，不会报错

## JS面向对象编程

在面向对象编程（OOP）中，对象是类的实例

在原型中声明的函数只会创建一次，所有实例共享；如果声明在构造函数内部，则每个实例都会创建自己的函数副本。使用原型的方式，可以节约内存和实例化开销

## 调试工具

通过调试可以观察到代码的执行流程以及赋值情况。在Chrome中通过F12打开开发者工具

## ESMAScript概述

ECMAScript是一种脚本语言规范，JavaScript是这个规范的一个实现

不同浏览器对JS的实现存在些许差异

新特性发布后，并非可以直接使用，还需等待浏览器支持。不过开发时完全可以直接使用新特性，通过Bable工具转化为ES5的等价代码

## ES6的功能

### 用let替代var声明变量

同一作用域中不可以重复声明相同的变量

存在暂时性死区，变量必须在使用前声明

有块级作用域，被`{}`包裹的部分

### 常量

它的行为和let一样，区别在于定义的变量是只读的，而且必须在声明时初始化

### 模板字面量

不必再拼接字符串

保持换行格式

通过`${}`插入变量

### 箭头函数

省去了function关键字

函数只有一条语句时，可以省去return

### 函数的参数默认值

没传实参时用默认值代替

### 声明展开和剩余参数

展开操作符`...`：

可以将数组作为参数，等价于`fun.apply(undefined, params)`

也可以代替arguments，当做剩余参数

数组解构：`let [x, y] = [...nums]`

对象简写：

```javascript
let name = 'Bob'
let person = {
  name
  say() {
    console.log('Hello World!')
  }
}
```

### 使用类进行面向对象编程

传统原型方式：

```javascript
function Book(title, pages) {
  this.title = title
  this.pages = pages
}
Book.prototype.printTitle = function () {
  console.log(this.title)
}
```

ES6简化语法：

```javascript
class Book {
  constructor(title, pages) {
    this.title = title
    this.pages = pages
  }
  printTitle() {
    console.log(this.title)
  }
}
```

ES6继承：

```javascript
class ITBook extends Book {
  constructor(title, pages, technology) {
    super(title, pages) // equial to Book.call(this, title, pages)
    this.technology = technology
  }
  printTechnoloty() {
    console.log(this.technology)
  }
}
```

尽管和其他面向对象的编程语言的语法很像，但还是基于原型实现的

使用属性存取器

```javascript
class Person {
  constructor(name) {
    this._name = name
  }
  get name() {
    return this._name
  }
  set name(value) {
    this._name = value
  }
}
```

和普通属性一样引用就可以执行get和set函数了

## ES7的功能

向下兼容性，即使更新到了新的标准，依然可以使用以前的规范特性

## 小结

温故而知新

