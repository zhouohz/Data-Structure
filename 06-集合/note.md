# 第6章 集合

**集合**是由一组无序且唯一（即不能重复）的项组成的

**空集**就是不包含任何元素的集合

## 构建数据集合

集合可以理解为没有重复元素且无序的数组

## 创建集合

Set类的框架

```javascript
class Set {
  constructor() {
    this.items = {}
  }
  add(value) {} // 添加一个新的项
  delete(value) {} // 移除一个值
  has(value) {} // 返回布尔值
  clear() {} // 移除集合中的所有项
  size() {} // 返回集合所包含元素的数量
  values() {} //返回包含所有值的数组
}
```

注意：这里使用对象作为基础结构，因为JS对象键不可重复（使键和值相同）。

### has(value)方法

首先实现 has 方法，因为 add、remove等方法中需要进行判断

```javascript
function has(value) {
  return value in this.items // 用JavaScript的in操作符来验证给定的值是否是items对象的属性
}
// 更好的实现方式
function has(value) {
  return this.items.hasOwnProperty(value) //返回一个表明对象是否具有特定属性的布尔值
}
```

### add(value)方法

```javascript
function add(value) {
  if(this.has(value)) return false
  this.items[value] = value
  return true
}
```

添加一个值的时候，把它同时作为键和值保存，因为这样有利于查找这个值。如果这个值是对象，那么键就是对应的引用

### remove和clear方法

```javascript
function remove(value) {
  if (!this.has(value)) return false
  delete this.items[value] // 将值也作为键的好处
  return true
}

function clear() {
  this.items = {} // 也可以迭代items使用remove方法移除
}
```

### size方法

使用 `Object.keys()` 或 `Object.values()` 实现

```javascript
function size() {
  return Object.keys(this.items).length
}
```

也可以和链表一样，添加 `this.length` 属性进行计数，当 add 或 remove 的时候更改

### values方法

需要使用`hasOwnProperty`方法（以验证`items`对象具有该属性），因为对象的原型包含了额外的属性（属性既有继承自JavaScript的`Object`类的，也有属于对象自身，未用于数据结构的）

```javascript
function values() {
  let result = []
  for (let value of this.items) {
    if (this.items.hasOwnProperty(value)) {
      result.push(value)
    }
  }
  return result
}
```

### 使用Set类

## 集合操作

### 并集

对于给定的两个集合，返回一个包含两个集合中所有元素的新集合。

```javascript
function union(otherSet) {
  let unionSet = new Set()
  this.values().forEach(item => {
    unionSet.add(item)
  })
  otherSet.values().forEach(item => {
    unionSet.add(item)
  })
  return unionSet
}
```

### 交集

对于给定的两个集合，返回一个包含两个集合中共有元素的新集合。

```javascript
function intersection(otherSet) {
  let intersectionSet = new Set()
  this.values().forEach(item => {
    if (otherSet.has(item)) {
      intersectionSet.add(item)
    }
  })
  return intersectionSet
}
```

### 差集

对于给定的两个集合，返回一个包含所有存在于第一个集合且不存在于第二个集合的元素的新集合。

```javascript
function difference(otherSet) {
  let differenceSet = new Set()
  this.values().forEach(item => {
    if (!otherSet.has(item)) {
      differenceSet.add(item)
    }
  })
  return differenceSet
}
```

### 子集

验证一个给定集合是否是另一集合的子集。

```javascript
function subset(otherSet) {
  if (this.size() > otherSet.size()) return false
  return this.values().every(item => {
    return otherSet.has(item)
  })
}
```

## ES6-Set类

区别：

1. ES6的`Set`的`values`方法返回`Iterator`，而不是值构成的数组

2. ES6的`Set`则有一个`size`属性，而不是`size()`
3. 用`delete(elem)`删除set中的元素

### ES6 Set类的操作

原生的Set并没有并集、交集、差集和子集等数学操作，需要自己写函数实现。在上面的基础上添加当前集合参数，替代`this`即可

## 小结

可以简化数组去重操作。将数组的值存入集合中，然后再通过`values()`取出来

