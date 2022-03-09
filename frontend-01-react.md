# React
React是一个用于构建用户界面的JavaScript库。开发者可以按需引入React特性，无论是给简单的HTML页面加一点交互还是完全由React驱动一个复杂应用。

## 特点
- 声明式。使用JSX/TSX语法，方便创建交互式UI。All-in-js。
- 组件化。每个React组件都是拥有/或不拥有自身状态的封装组件，对其组合以构成复杂的UI。
- 跨平台。React还可使用Node做服务器渲染，或使用React Native开发原生移动应用。

## 核心概念
### 01 组件
函数组件和Class组件
1. 函数组件，接收唯一带有数据的props对象并返回一个React元素。也可以用es6 class来声明组件。这两种方式在react中是等效的。
2. 根据[这篇文章](https://overreacted.io/how-are-function-components-different-from-classes/)可知，
类组件中使用this读取props和state，而this是mutable的，react总是会改变它使得它保持最新，那么在类中读取props或state的值时，就需要多加注意了。
相比之下，函数组件通过传值调用，不会遇到这个问题。但有时候我们也想在函数组件中获取最新值，可以用useRef解决。

受控组件和非受控组件

1. [受控组件](https://zh-hans.reactjs.org/docs/forms.html#controlled-components)：在HTML中，表单元素（如\<input\>、<textarea>、\<select\>）通常自己维护state，并根据用户输入进行更新。而在React中，可变状态（mutable state）通常保存在组件的state属性中，并且只能通过使用setState()来更新。我们把这两者结合，使得React的state成为唯一数据源。渲染表单的React组件还控制着用户输入过程中表单发生的操作。被React以这种方式控制取值的表单输入元素就称为受控组件。
  
2. [非受控组件](https://zh-hans.reactjs.org/docs/uncontrolled-components.html)：不使用React的state作为表单输入元素的唯一数据源，不为每个元素状态更新都编写数据处理函数。而是通过ref获取元素自身的state。*在React中，<input type="file"/>始终是一个非受控组件。
  
[在什么场景下使用受控组件/非受控组件](https://goshacmd.com/controlled-vs-uncontrolled-inputs-react/)

[受控组件 & 非受控组件](https://www.baobangdong.cn/controlled-components-and-uncontrolled-components/)

高阶组件 & Render Props

1. 高阶组件是参数为组件，返回值为新组件的函数。组件是将 props 转换为 UI，而高阶组件是将组件转换为另一个组件。
2. HOC不是React API的一部分，它是一种基于React的组合特性形成的设计模式。
3. 为什么使用高阶组件？

### 02 合成事件

### 03 Context
  
### 04 refs
Refs转发
  
Refs&DOM

回调Refs

## React-Hooks
Q1：为什么需要React-Hooks？
> A：1⃣️ 组件之间复用状态逻辑很难。React没有提供将可复用性行为“附加”到组件的途径。Hook可以从组件中提取状态逻辑，使得这些逻辑可以单独测试并复用。让我们在无需修改组件结构的情况下复用状态逻辑。2⃣️ 复杂组件让人难以理解。比如我们常常需要在不同的生命周期函数获取数据或是注册/清除订阅，这意味着相关联的逻辑被不自然地拆分到了不同的生命周期函数中。另一方面，类组件难以拆分为更小的粒度，因为状态逻辑无处不在。所以很多人将React和状态管理库结合，但这又引入了新的抽象概念，需要在不同的文件中切换，使得复用更加困难。Hook将组件中相互关联的部分拆分成更小的函数，而非强制按照生命周期划分。还可以用reducer来管理组件的内部状态，使其更加可预测。3⃣️ Hook使你在非class的情况下可以使用更多的React特性。[官方文档](https://zh-hans.reactjs.org/docs/hooks-intro.html)
>

### hook API
| 名称 | 常用 | 用途 | 备注 |
|:--- | --- | --- | --- |
| useState | basic | 接收初始值，返回一个state，以及更新state的函数 | |
| useEffect | basic | 接收一个包含命令式、且可能有副作用代码的函数 | |
| useContext | basic | 接收一个 context 对象（React.createContext 的返回值）并返回该 context 的当前值 | |
| useReducer | advanced | `const [state, dispatch] = useReducer(reducer, initialArg, init);` | useState的替代方案 |
| useCallback | advanced | 接收内联回调函数及依赖项数组，返回一个 memoized 回调函数 | 该回调函数仅在某个依赖项改变时才会更新；`useCallback(fn, deps)`相当于`useMemo(() => fn, deps)` |
| useMemo | advanced | 接收“创建”函数和依赖项数组，返回一个 memoized 值 | 仅会在某个依赖项改变时才重新计算 memoized 值，避免重复计算 |
| useRef | advanced | 返回一个可变的ref对象，其 .current 属性被初始化为传入的参数（initialValue）| 返回的ref对象在组件的整个生命周期内持续存在；useRef可以很方便的保存任何可变值 |
| useImperativeHandle | advanced | `useImperativeHandle(ref, createHandle, [deps])`，使用 ref 时自定义暴露给父组件的实例值 | useImperativeHandle 应当与 forwardRef 一起使用 |
| useLayoutEffect | advanced | 会在所有的 DOM 变更之后同步调用 effect | 在浏览器执行绘制之前，useLayoutEffect 内部的更新计划将被同步刷新 |
| useDebugValue | advanced | 用于在 React 开发者工具中显示自定义 hook 的标签 | 延迟格式化 debug 值 |

## React 路由
- [react-router](https://reactrouter.com/)，全特性客户端/服务端路由库for React。
- [reach router](https://github.com/reach/router)，下一代React路由。

Q1：前端路由的几种模式的区别？[前端路由](https://github.com/Noa-p/myblog/blob/main/frontend-03-router.md)

Q2：如果让你设计一个前端路由库，你会怎么考虑？

## React 状态管理
当项目规模增大，需要管理的状态（如服务器响应、缓存数据、在本地生成尚未持久化到服务器的数据、UI状态等）也越来越多，如果一个model的变化会引起另一个model的变化，当view变化时，可能引起一个model及另一个model的变化，甚至引起另一个view的变化。让state在什么时候，由于什么原因、如何变化变得不可控。
  
前端新需求的复杂性很大程度来自：我们常常将“变化”和“异步”两个概念搞混。一些库如React试图在View层禁止异步和直接修改DOM来解决这个问题，但处理state的任务依然存在。状态管理库就是为了帮助解决这个问题被开发出来的。
  
- [Redux](https://github.com/Noa-p/myblog/blob/main/frontend-01-redux.md)，JS 应用的状态容器，提供可预测的状态管理
- MobX，简单，可扩展的状态管理库
- Recoil，React 状态管理库
  
并不是所有的项目都需要状态管理库，利用 React Context 或者 react-query 这类接口请求库即可满足部分需求。
  
## React 接口请求
- axios，传统接口请求库
- react-query，用于获取、缓存和更新 React 中异步数据的 Hooks 接口请求库
- swr，用于数据请求的 React Hooks 库

## React 单测
- jest，优雅、简洁的 JavaScript 测试框架，单测必选项
- react-testing-library，简单且完整的 React DOM 测试工具

## React SSR
- nest.js，一个渐进式的 Node.js 框架，用于构建高效、可靠和可扩展的服务端应用。

## React 原理
- [Immutability in React and Redux: The Complete Guide](https://daveceddia.com/react-redux-immutability-guide/)

## 常见问题
Q：setState是同步还是异步？







