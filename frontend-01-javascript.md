# JavaScript
## 数据类型
### 基本数据类型，值类型vs引用类型
`JS 8中基础数据类型：Undefined、Null、Boolean、Number、String、Object、Symbol、BigInt`
- Symbol 表示独一无二的值，最大的用法是用来定义对象的唯一属性名
- BigInt 表示任意大小的整数

值类型vs引用类型
- 值类型
  - 直接存储在栈（自动分配的内存空间，系统自动释放）中，占据空间小、大小固定，属于被频繁使用的数据；
  - **基本数据类型的值不可变**
  - 基本数据类型的比较是值的比较，最好使用严格等于，因为`==``是会进行类型转换的
  - 基本数据类型的赋值是传值，在内存中新开辟一段栈内存，然后再将值赋值到新的栈中
- 引用类型
  - 在栈中存储地址，实际对象存储在堆（动态分配的内存，大小不定且不会自动释放）中，占据空间大，大小不固定。如果存储在栈中，会影响程序运行的性能
  - 引用类型的值是可变的
  - 引用类型的比较是引用的比较
  - 引用类型的赋值是传址，只是改变指针的指向
  - 浅拷贝、深拷贝

[处理技巧汇总](https://github.com/Noa-p/algorithm-learning/issues/75)

### 深拷贝

### 0.1+0.2 ! == 0.3

## 原型和原型链
## 作用域和作用域链
## 执行上下文
## 闭包
## call、apply、bind的实现
## new 实现
## 异步操作
JavaScript是单线程的。通过事件循环机制来来实现异步操作。

### 事件循环机制
事件循环机制中，负责执行JS脚本的单线程我们称为主线程，在内存中表现为一个执行栈，JS只通过主线程执行任务。异步任务被挂起，存储在堆中，当异步任务准备就绪，它对应的事件便进入任务队列。主线程首先执行同步任务，然后查看任务队列是否有就绪的异步任务（或者时间到了的异步任务），将它重新进入主线程，调用相应的回调函数执行。至此即完成一轮事件循环。引擎会不断的去任务队列检查满足条件的异步任务。

### 同步任务 & 异步任务
异步任务指被JS引擎放在一边，不进入主线程而进入任务队列的任务。

### 宏任务 & 微任务
宏任务指需要调用浏览器接口完成的任务，微任务只JavaScript自身的异步操作。宏任务总是在下一轮事件循环中执行，微任务在本轮事件循环最后执行。
- 宏任务：setTimeout()、setInterval()、Ajax、DOM操作
- 微任务：Promise、Async/await

Q：[查看下列代码，打印顺序如何？](https://github.com/Noa-p/myblog/issues/3)

### 异步操作的模式
- 回调函数：在一个函数执行之后调用的函数。简单，易于理解，但不易维护，耦合性强。
- 事件监听：事件驱动模式。不取决于代码的顺序，而取决于事件是否发生。易于理解，可绑定多个事件，每个事件可以指定多个回调函数，去耦合，利于模块化。缺点是整个程序都要变成事件驱动型，难以看出主流程。
- 发布/订阅：存在信号中心，任务执行完成向中心发送信号，其他任务可以从信号中心订阅这个信号。可监控。

### 异步操作的流程控制
- 串行执行
- 并行执行
- 并行与串行的结合

## 浏览器垃圾回收机制
## 实现一个EventEmitter类

## 常见问题
Q1：为什么class中需要在constructor中这样写？`this.foo = this.foo.bind(this);`
> A: 和普通函数一样，类方法的this值取决于它们如何被调用。在类构造函数中将类方法的this值总是指向这个类实例，可以避免一些异常。
> [类中的this](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this#%E7%B1%BB%E4%B8%AD%E7%9A%84this)
> 
> 这种绑定this的方式和箭头函数又存在区别。这种方法将类方法挂载到当前对象的原型上。如果使用箭头函数，这个方法属于实例方法，会挂载到每个实例上。
> 假设组件被复用多份，每个实例对象都会重新定义开辟foo方法需要的内存。
> [在 constructor 中 bind this 的优点](https://liaoyinglong.github.io/blog/src/react/01.%E5%9C%A8constructor%E4%B8%ADbind%20this%E7%9A%84%E4%BC%98%E7%82%B9/)

Q2: 什么是闭包？



