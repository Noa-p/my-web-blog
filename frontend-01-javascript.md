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
## 异步
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



