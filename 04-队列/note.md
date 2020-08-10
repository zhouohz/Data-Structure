# 第四章 队列

## 队列数据结构

队列是遵循FIFO（First In First Out，先进先出，也称为先来先服务）原则的一组有序的项。队列在尾部添加新元素，并从顶部移除元素。最新添加的元素必须排在队列的末尾。

## 创建队列

```javascript
function Queue() {
  this.items = []
}
```

### 向队列添加元素

```javascript
Queue.prototype.enqueue = function (element) {
  this.items.push(element)
}
```

### 从队列移除元素

```javascript
Queue.prototype.dequeue = function () {
  return this.items.shift()
}
```

### 查看队列头元素

```javascript
Queue.prototype.front = function () {
  return this.items[0]
}
```

### 检查队列是否为空

```javascript
Queue.prototype.isEmpty = function () {
  return this.items.length === 0
}
```

### 打印队列元素

```javascript
Queue.prototype.print = function () {
  console.log(this.items.toString())
}
```

## 用ES6语法实现的Queue类

我们要用一个WeakMap来保存私有属性items，并用外层函数（闭包）来封装Queue类

```javascript
const Queue = (function () {
  const items = new WeakMap()
  class Queue {
    constructor() {
      items.set(this, [])
    }
    enqueue(element) {
      items.get(this).push(element)
    }
    dequeue() {
      return items.get(this).shift()
    }
  }
  return Queue
})()
```

## 优先队列

实现一个优先队列，有两种选项：设置优先级，然后在正确的位置添加元素；或者用入列操作添加元素，然后按照优先级移除它们. 下例采用第一种方案:

```javascript
// 优先级的数值越小, 优先级越高, 称为最小优先队列
class PriElem {
  constructor(element, priority) {
    this.element = element
    this.priority = priority
  }
}
const PriorityQueue = (function () {
  const items = new WeakMap()
  class PriorityQueue {
    constructor() {
      items.set(this, [])
    }
  }
  enqueue(element, priority) {
    const newElem = new PriElem(element, priority)
    // 在插入的时候, items已经是按从小到大排列了
    let itemsArr = items.get(this)
    let isInsert = false
    for (let i = 0; i < itemsArr.length; i++) {
      if (priority < itemsArr[i].priority) {
        itemsArr.splice(i, 0, newElem)
        thisInsert = true
        break
      }
    }
    // 当队列为空时会跳过for循环, 执行if里的代码
    if (!isInsert) itemsArr.push(newElem)
  }
  print() {
    items.get(this).forEach(item => {
      console.log(`${item.element} -> ${item.priority}`)
    })
  }

  // 其他方法相同哦
})()
```

## 循环队列

```javascript
let names = ['John','Jack','Camila','Ingrid','Carl']

function hotPotato(names, step) {
  let nameList = new Queue()
  names.forEach(item => {
    nameList.enqueue(item)
  })
  while(nameList.size() > 1) {
    for (let i = 0; i < step; i++) {
      nameList.enqueue(nameList.dequeue())
    }
    console.log(`被淘汰的人是: ${nameList.dequeue()}`)
  }
  console.log(`获胜者是: ${nameList.dequeue()}`)
}

```

## JS任务队列

JS是单线程的, 通过任务队列来依次执行任务, 异步的事件交给浏览器去等待, 完成后添加到任务队列, 避免等待.

## 小结

受限的线性表
