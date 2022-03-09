# 浏览器模型

## 01 网页嵌入代码
- script元素嵌入代码
- script元素加载外部脚本
- 事件属性
- URL协议 - `javascript:`协议

### script元素
- 浏览器解析HTML文件时，发现<script>元素，会暂停解析，把网页渲染的控制权转交给JS引擎
- 如果<script>元素引用了外部脚本，就下载该脚本再执行，否则就直接执行代码
- JS引擎执行完毕，控制权交还渲染引擎，恢复往下解析HTML网页
- 对于来自同一个域名的资源，浏览器有限制，同时最多下载6-20个资源，即同时打开的TCP连接有限制
  
阻塞效应
- 如果有多个script标签，浏览器会并行下载，但执行顺序与出现顺序一致
- 解析和执行CSS也会产生阻塞。不同浏览器有不同的策略，Firefox会等到前面的样式表都下载并解析完，再执行脚本；
  Webkit则是一旦发现脚本引用了样式，就会暂停执行脚本，等到样式表下载并解析完，再恢复执行

defer属性
- 延迟脚本的执行，等到 DOM 加载生成后，再执行脚本。下载脚本文件时不会阻塞页面渲染。
  下载的脚本文件在`DOMContentLoaded`事件触发前执行。且保证顺序。

async属性
- 使用另一个进程下载脚本，下载完成后理解执行。无法保证顺序
  
动态加载
- 动态生成然后嵌入页面，这样不会阻塞页面渲染，但是无法保证顺序。手动设置`script.async`为`false`。

加载使用的协议
- 默认是http，如用https，需要写明
  
## 02 浏览器的组成
核心：渲染引擎 & JavaScript引擎
### 渲染引擎
> 将网页代码渲染为用户视觉可以感知的平面文档

不同浏览器有不同的渲染引擎：
- Firefox: Gecko引擎
- Safari: WebKit引擎
- Chrome: Blink引擎
- IE: Trident引擎
- Edge: EdgeHTML引擎

渲染引擎处理网页的四个阶段：
1. 解析代码：HTML解析为DOM，CSS代码解析为CSSOM
2. 对象合成：将DOM和CSSOM合成一棵渲染树
3. 布局：计算出渲染树的布局Layout
4. 绘制：将渲染树绘制到屏幕

重流和重绘

渲染树转换为网页布局，称为“布局流”（flow）；布局显示到页面的这个过程，称为“绘制”（paint）。有阻塞效应。
页面生成后，脚本操作、样式表操作、用户交互都可能出发重流和重绘。

Q：开发者需要设法降低重绘的的次数和成本。怎么做？

### JavaScript引擎
> 读取网页中的JavaScript代码，处理并运行。

现代浏览器都将JS进行一定程度的编译，生成类似字节码的中间代码，以提高运行速度。

早期浏览器内部对JS的处理过程如下：
1. 读取代码，词法分析（Lexical analysis），将代码解成词元（token）
2. 对词元进行语法分析（parsing），生成语法树（syntax tree）
3. 使用解释器（translator），将代码转成字节码（bytecode）
4. 使用字节码解释器（bytecode interpreter），将字节码转成机器码

逐行解释将字节码转为机器码是低效的，为了提高运行速度，现代浏览器改为采用“即时编译”（JIT），
即字节码只在运行时编译，用到哪一行就编译哪一行，并把编译结果缓存（inline cache）。
字节码不能直接运行，而是运行在一个虚拟机之上（Virtual Machine），一般也把虚拟机称为JavaScript引擎。
有的JavaScript虚拟机基于字节码，有的基于源码。[<sup>[1]</sup>](#refer-anchor-1)

常见JavaScript引擎：
- IE: Chakra
- Safari: Nitro/JavaScript Core
- Opera: Carakan
- Firefox: SpiderMonkey
- Chrome: V8

## 03 Web存储
cookie、localStorage、sessionStorage
cookie
- 由服务器设置，用于浏览器和server通讯
- cookie元数据：Cookie 的名字、值、到期时间、所属域名、生效的路径
- 存储大小限制为4kb
- 只能通过`document.cookie = ''`来操作
- 通常用于保存用户登录信息、个性化信息、追踪用户，由于HTTP是无状态的
- 受同源政策影响

localStorage & sessionStorage
- HTML5为存储设计，不会随着HTTP请求发送到服务端
- 以键值对的方式存储
- 最大可存5M
- 浏览器提供Web storage API，简单易用
- 通常用于保存一些网页的状态信息
- 受同源政策影响

它们的区别
- localStorage数据永久存储在客户端本地，除非代码删除或手动删除
- sessionStorage数据只存在于当前会话，当前窗口关闭则清空

## 04 同源政策
> 为了保证用户信息的安全，防止恶意的网站窃取数据

限制范围：
> - 无法读取非同源网页的cookie、localStorage和indexedDB
> - 无法接触非同源网页的DOM
> - 无法向非同源地址发送AJAX请求，可以发送但浏览器会拒绝接收响应

另外，js脚本可以拿到其他窗口的window对象。但如果非同源，也是有限制的。只允许接触九个属性、四个方法。

### 如何实现跨域？
- document.domain 设置相同 // 可以获取cookie和iframe窗口
- 片段标识符传递信息 // 可以共享localStorage
- window.postMessage()
- jsonp // ajax
- websocket
- cors - http请求头

  
## 参考
<div id="refer-anchor-1"></div>

- [1] [浏览器模型](https://wangdoc.com/javascript/bom/index.html)
