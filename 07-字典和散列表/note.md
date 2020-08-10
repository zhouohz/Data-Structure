# 第7章 字典和散列表

使用字典和散列表来存储唯一值

## 字典

在字典中，存储的是[键，值]对，其中键名是用来查询特定元素的。字典和集合很相似，集合以[值，值]的形式存储元素，字典则是以[键，值]的形式来存储元素。字典也称作映射。

### 创建字典

Dictionary框架

```javascript
class Dictionary {
  constructor() {
    this.items = {}
  }
  set(key, value) {}
  delete(key) {}
  has(key) {}
  get(key) {}
  clear() {}
  size() {}
  keys() {}
  values() {}
}
```

### has和set方法

```javascript
function has(key) {
  return this.items.hasOwnProperty(key)
  // return key in this.items
}

function set(key, value) {
  if (this.has(key)) return false
  this.items[key] = value
  return true
}
```

### delete方法

```javascript
function delete(key) {
  if (!this.has(key)) return false
  delete this.items[key]
  return true
}
```

### get和values方法

```javascript
function get(key) {
  // 如果key不存在，会返回undefined
  return this.items[key]
}

function values() {
  let values = []
  for (let value of this.items) {
    values.push(value)
  }
  return values
}
// keys()同理。也可以用Object的keys和values方法获取
```

### 使用Dictionary类

存储一些联系人（人名：邮箱）

## 散列表

它是字典的一种散列表实现方式

散列算法的作用是尽可能快地在数据结构中找到一个值。在之前的章节中，你已经知道如果要在数据结构中获得一个值（使用get方法），需要遍历整个数据结构来找到它。如果使用散列函数，就知道值的具体位置，因此能够快速检索到该值。散列函数的作用是给定一个键值，然后返回值在表中的地址。

### 创建散列表

散列表的框架

```javascript
class HashMap {
  constructor() {
    this.table = []
  }
  put(key, value) {}
  remove(key) {}
  get(key) {}
}
```

### 实现散列函数

它是HashMap类的一个私有方法。用闭包将它与class封装在一起

```javascript
function loseloseHashCode(key) {
  let hashcode = 0
  for (let i = 0; i < key.length; i++) {
    hashcode += key.charCodeAt(i)
  }
  return hashcode % 37 // 防止值过大,除数为质数且稍大于散列表的length。
}
```

### 实现put、get和remove方法

```javascript
function put(key, value) {
  const position = loseloseHashCode(key)
  this.table[position] = value
}

function get(key) {
  return this.table[loseloseHashCode(key)]
}
function remove(key) {
  this.table[loseloseHashCode(key)] = undefined
}
```

注意：这里不能使用splice等方法进行删除，需要保留位置，防止下标更改，导致散列函数的对应关系错乱

### 使用HashTable类

### 散列表和散列集合

在一些编程语言中，还有一种叫作散列集合的实现。散列集合由一个集合构成，但是插入、移除或获取元素时，使用的是散列函数。我们可以重用本章中实现的所有代码来实现散列集合，不同之处在于，不再添加键值对，而是只插入值而没有键。例如，可以使用散列集合来存储所有的英语单词（不包括它们的定义）。和集合相似，散列集合只存储唯一的不重复的值。

### 处理散列表中的冲突

有时候，一些键会有相同的散列值。不同的值在散列表中对应相同位置的时候，我们称其为冲突

处理冲突的几种方法：分离链接、线性探查和双散列法

#### 分离链接

散列表（数组）的每个位置存放一个链表，相同散列值的的数据链接到链表中。

创建一个ValuePair类用于保存key和value，同时作为LinkedList的节点元素

```javascript
class ValuePair {
  constructor(key, value) {
    this.key = key
    this.value = value
  }
}
```

同时需要

#### 线性探查

### 创建更好的散列函数

表现良好的散列函数是由几个方面构成的：插入和检索元素的时间（即性能），当然也包括较低的冲突可能性。

## ES6-Map类

## ES6-WeakMap类和WeakSet类

## 小结


