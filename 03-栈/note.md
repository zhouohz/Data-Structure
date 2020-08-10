# 第三章 栈

## 栈数据结构

**栈**是一种遵从**后进先出**（LIFO）原则的有序集合。新添加的或待删除的元素都保存在栈的同一端，称作栈顶，另一端就叫栈底。在栈里，新元素都靠近栈顶，旧元素都接近栈底。

### 创建栈

```javascript
function Stack() {
  // 数组末尾为栈顶
  this.items = []
}
Stack.prototype.push = function (element) {}
Stack.prototype.pop = function () {}
Stack.prototype.peek = function () {}
Stack.prototype.isEmpty = function () {}
Stack.prototype.clear = function () {}
Stack.prototype.size = function () {}
```

### 向栈添加元素

```javascript
Stack.prototype.push = function (element) {
  this.items.push(element)
}
```

### 从栈移除元素

```javascript
Stack.prototype.pop = function () {
  return this.items.pop()
}
```

### 查看栈顶元素

```javascript
Stack.prototype.peek = function () {
  let length = this.items.length
  return this.items[length - 1]
}
```

### 检查栈是否为空

```javascript
Stack.prototype.isEmpty = function () {
  return this.items.length === 0
}
```

```javascript
Stack.prototype.size = function () {
  return this.items.length
}
```

### 清空和打印栈元素

```javascript
Stack.prototype.clear = function () {
  this.items = []
}
```

```javascript
Stack.prototype.print = function () {
  console.log(this.items.toString())
}
```

## ES6和Stack类

### 用ES6语法声明Stack类

基础写法

```javascript
class Stack {
  constructor () {
    this.items = []
  }
  push(element) {
    this.items.push(element)
  }
}
```

存在的问题：items不是私有属性，用户可以直接访问，破坏栈结构

用ES6新增的Symbol基本类型替代

```javascript
let _items = Symbol()
class Stack {
  constructor() {
    this[_items] = []
  }
}
```

这种方法创建了一个假的私有属性，因为ES6新增的`Object.getOwnPropertySymbols`方法能够取到类里面声明的所有`Symbols`属性

用ES6的WeakMap实现类

WeakMap可以存储键值对，其中键是对象，值可以是任意数据类型

```javascript
const items = new WeakMap()
class Stack {
  constructor () {
    items.set(this, [])
  }
  push(element) {
    let s = items.get(this)
    s.push(element)
  }
}
```

最后用立即执行函数封装起来防止items的改动：

```javascript
let Stack = (function () {
  const items = new WeakMap()
  class Stack {
    constructor () {
      items.set(this, [])
    }
    push(element) {
      let s = items.get(this)
      s.push(element)
    }
  }
  return Stack
})()
```

尽管ES6引入了类的语法，我们仍然不能像在其他编程语言中一样声明私有属性或方法。有很多种方法都可以达到相同的效果，但无论是语法还是性能，这些方法都有各自的优点和缺点。

## 用栈解决问题

它可以存储访问过的任务或路径、撤销的操作等；Java和C#用栈来存储变量和方法调用，特别是处理递归算法时，有可能抛出一个栈溢出异常

### 进制转化

```javascript
function baseConverter(decNumber, base) {
  let remStack = new Stack()
  let digits = '0123456789ABCDEF'
  while (decNumber !== 0) {
    remStack.push(decNumber % base)
    decNumber = Math.floor(decNumber / base)
  }
  let result = []
  while (!remStack.isEmpty()) {
    result.push(digits[remStack.pop()])
  }
  return result.join('')
}
```

## 小结

受限制的线性表，只能从一端进出