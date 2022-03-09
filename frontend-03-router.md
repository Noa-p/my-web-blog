# 前端路由

Ajax的出现催生了SPA，只有一个HTML页面，一旦页面加载完成，SPA不会因为用户的操作而进行页面的加载和跳转，取而代之的是利用JS动态的变换HTML的内容，从而模拟多个视图间跳转。对于SPA来说，页面的切换就是视图之间的切换。

但SPA存在两个问题：
1. SPA无法记住用户的操作记录，无论刷新、前进还是后退，都无法展示用户真实的期望内容
2. SPA中虽然由于业务的不同有多种页面展示形式，但只有一个URL，对SEO不友好，不方便搜索引擎进行收录

前端路由解决上述问题。

## 什么是前端路由？
> 保证只有一个HTML页面，且与用户交互时不刷新和跳转页面的同时，为SPA中的每个视图展示形式匹配一个特殊的URL。在刷新、前进、后退和SEO时均通过这个特殊的URL来实现。需要做到：
> 1. 改变URL且不让浏览器向服务器发送请求
> 2. 可以监听到URL的变化

### hash模式
片段标识符。hash值的变化不会导致浏览器向服务器发送请求，且hash的改变会出发hashchange事件，浏览器的前进后退可以控制。

### history模式
禁用a标签默认行为，利用HTML5提供的history API（history.pushState, history.replaceState, history.state）控制路由。

### 如何抉择？
hash模式的优点：
- 兼容性更好，可以兼容到IE8
- 无需服务端配合处理非单页的URL地址，history模式需要 `怎么做？？`

hash模式的缺点：
- 看起来丑
- 会导致锚点功能失效
- 相同hash值不会触发动作将记录加入到历史栈中，但pushState可以

[自己实现一个前端路由类](https://github.com/Noa-p/build-my-own-xx/tree/main/router)

## 路由库
- react-router，全特性客户端/服务端路由库for React
- reach router，下一代React路由
- vue-router

### React-Router

## 参考
[1] [「前端进阶」彻底弄懂前端路由](https://juejin.cn/post/6844903890278694919)

[2] [React-Router - Main Concepts](https://reactrouter.com/docs/en/v6/getting-started/concepts)

