# 第二章 数组

在JS中数组能存储不同类型的数据，但不推荐这么做

## 为什么用数组

假设需要保存当前城市每个月的平均温度。

可以为每个月创建一个变量，但是，当数据量变多时，就不便于管理了

此时，就可以用到数组，更加简洁的呈现相同的信息

## 创建和初始化数组

```javascript
let foo = new Array()
let foo = new Array(5)
let foo = new Array('a', 'b', 'c')
let foo = []
let foo = ['a', 'b', 'c']
```

访问元素和迭代数组

```javascript
for (let i = 0; i < foo.length; i++) {
  console.log(foo[i])
}
```

## 添加元素

在数组末尾添加一个元素

```javascript
let foo = [0, 1, 2, 3, 4]
foo[foo.length] = 5
```

在JS中，数组是一个可以修改的对象，添加或删除元素时，它会动态增长

### 使用push方法

向数组的末尾添加任意个元素

```javascript
foo.push(6, 7)
```

### 插入元素到数组首位

可以将数组中的每个元素向后移动一位，将元素赋值到索引为0处

```javascript
for (let i = foo.length; i > 0; i--) {
  foo[i] = foo[i - 1]
}
foo[0] = element
```

使用unshift方法。同push方法一样，在数组开头插入任意个元素

## 删除元素

用pop方法删除数组末尾的元素

Tips：通过push和pop方法可以用数组模拟栈

和插入时一样，可以将元素依次向前移动一位，进行覆盖删除，但是数组长度不变。使用shift方法可以切实的删除数组的第一个元素

Tips：通过shift和push方法可以用数组模拟队列

## 在任意位置添加或删除元素

使用splice方法

```javascript
foo.splice(3) // 从第三个元素删到末尾
foo.splice(3, 1) // 从第三个元素开始删，删除一个元素
foo.splice(3, 1, 'a', 'b') // 。。。在删除处的前面插入任意个元素
```

补充：可以用`delete foo[2]`的方式删除元素，等价于`foo[2] = undefined`。不推荐使用

## 二维和多维数组

JS原生不支持矩阵，但可以用数组套数组的形式，实现矩阵或多维数组

### 迭代二维数组元素

```javascript
for (let row = 0; row < Matrix.length; row++) {
  for (let col = 0; col < Matrix[row].length; col++) {
    console.log(Matrix[row][col])
  }
}
```

### 多维数组

同理，继续嵌套循环即可

## JS的数组方法参考

### 数组合并

```javascript
let zero = 0
let positiveNumbers = [1, 2, 3]
let negativeNumbers = [-1, -2, -3]
let result = negativeNumbers.concat(zero, positiveNumbers)
```

可以接受数组或元素，返回一个新的数组

### 迭代器函数

every方法：迭代数组中的每个元素，直到回调函数返回false

some方法：迭代数组中的每个元素，直到回调函数返回true

forEach方法：迭代整个数组，和for循环的结果相同。注意：无法控制循环变量

map方法：返回一个新数组，保存的是回调函数的返回值

filter方法：返回一个新数组，当回调函数返回true时，就将当前遍历项添加到新数组

reduce方法：reduce方法接收一个函数作为参数，这个函数有四个参数：previousValue、currentValue、index和array。这个函数会返回一个将被叠加到累加器的值，reduce方法停止执行后会返回这个累加器；reduce方法的第二个参数为previousValue的初始值

### ES6和数组的新功能

使用for...of循环迭代：遍历项为值。而for...in循环的遍历项为索引

使用ES6新的迭代器：ES6为Array类新增了iterator属性，需要通过Symbol.iterator访问

```javascript
let iterator = nums[Symbol.iterator]()
console.log(iterator.next().value) // 第一个元素
console.log(iterator.next().value) // 第二个元素
console.log(iterator.next().value) // 遍历完成是输出undefined
```

不断调用next方法，就能得到数组中的值，等价于values方法（返回值的迭代器）

数组的entries、keys和values方法：分别返回键值对的迭代器，键的迭代器，值的迭代器

Array.from方法：根据已有的数组创建一个新数组。和map方法类似

Array.of方法：根据传入的参数创建一个新数组。等价于字面量创建数组。

fill方法：用静态值填充数组。`nums.fill(0, 1, 5)`：静态值为0，从索引1填充到5，不包括5

copyWithin方法：复制数组中的一系列元素到同一数组指定的起始位置。

```javascript
let nums = [0, 1, 2, 3, 4, 5]
nums.copyWithin(0, 3, 5) // 从索引0开始，依次赋值第3-5个元素（不包括5）
console.log(nums) // [3, 4, 2, 3, 4, 5]
```

### 排序元素

reverse方法：反序数组元素

sort方法：默认将元素当成字符串，按ASCII码进行比较，可以传入一个比较函数，当返回值为正时交换比较元素的位置，否则不换，内部采用的是冒泡排序方法

### 搜索

indexOf方法：返回与参数匹配的第一个元素的索引

lastIndexOf方法：返回与参数匹配的最后一个元素的索引，逆向搜索

find方法：接收一个回调函数，搜索一个满足回调函数条件的值，否则返回undefined

findIndex方法：接收一个回调函数，搜索一个满足回调函数条件的值对应的索引，否则返回-1

includes方法：如果数组里存在某个元素，includes方法会返回true，否则返回false，第二个参数可以指定查找的起始索引

### 输出数组为字符串

使用toString方法，元素间用逗号间隔

join方法：可以指定元素间的间隔符

## 类型数组

与C和Java等其他语言不同，JavaScript数组不是强类型的，因此它可以存储任意类型的数据。

而类型数组则用于存储单一类型的数据。它的语法是let myArray = new TypedArray (length)

## 小结

理解好回调函数
