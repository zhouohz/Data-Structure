# 第五章 链表

## 链表数据结构

|      | 优点                             | 缺点                 |
| ---- | -------------------------------- | -------------------- |
| 数组 | 随机存取                         | 增删的成本高         |
| 链表 | 添加或删除元素不需要移动其他元素 | 访问元素需要从头遍历 |



## 创建链表

LinkedList 类的骨架:

```javascript
class Node {
  constructor(element) {
    this.elem = element
    this.next = null
  }
}

class LinkedList {
  constructor() {
    this.head = null
    this.length = 0
  }
  append(element) {}
  inset(position, element) {}
  removeAt(position) {}
  remove(element) {}
  indexOf(element) {}
  isEmpty() {}
  size() {}
  getHead() {}
  print() {}
}
```

### 向链表尾部追加元素

```javascript
function append(element) {
  const newElem = new Node(element)
  if (this.isEmpty()) {
    this.head = newElem
  }else {
    let lastElem = this.head
    while(lastElem.next) {
      lastElem = lastElem.next
    }
    lastElem.next = newElem
  }
  this.length++
}
```

### 从链表中移除元素

从特定位置移除一个元素

```javascript
function removeAt(position) {
  if (position < 0 || position > this.length) return null
  let removeElem = null
  if (position === 0) {
    removeElem = this.head
    this.head = removeElem.next
  }else {
    let previousElem = this.head
    // 移动到被删除元素的前一位, position至少为1
    for (let i = 0; i < position - 1; i++) {
      previousElem = previousElem.next
    }
    removeElem = previousElem.next
    previousElem = removeElem.next
  }
  this.length--
  return removeElem.elem
}
```

### 在任意位置插入元素

```javascript
function insert(position, element) {
  if (position < 0 || position > this.length) return false
  const newElem = new Node(element)
  if (positon === 0) {
    newElem.next = this.head
    this.head = newElem
  }else {
    let previousElem = this.head
    for (let i = 0; i < position - 1; i++) {
      previousElem = previousElem.next
    }
    newElem.next = previous.next
    previous.next = newElem
  }
  this.length++
  return true
}
```

### 实现其他方法

```javascript
function print() {
  let result = [], current = this.head
  while (current !== null) {
    result.push(current.elem)
    current = current.next
  }
  console.log(result)
}

function indexOf(element) {
  let current = this.head, index = 0
  while(current !== null && current.elem !== element) {
    current = current.next
    index++
  }
  if (!current) return -1
  return index
}

// 找索引 + 删除特定位置元素 = 删除特定元素
function remove(element) {
  const index = this.indexOf(element)
  return this.removeAt(index)
}

function isEmpty() {
  return this.length === 0
}
```

## 双向链表

节点类新增`this.prev`指向前一个节点; DoublyLinkedList类新增`this.tail`指向最后一个节点, 便于遍历

### 在任意位置插入新元素

### 从任意位置移除元素

## 循环链表

单向循环链表: 最后一个节点的next指向头节点

双向循环链表: 最后一个节点的next指向头节点, 且头节点的prev指向尾节点

## 小结

无需移动链表中的元素，就能轻松地添加和移除元素
