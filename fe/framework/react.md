## Vue vs React 

[Vue 和 React 的优点分别是什么？](https://www.zhihu.com/question/301860721/answer/724759264)

## 生命周期

constructor -> getDerivedStateFromProps -> componentDidMount -> shouldComponentUpdate -> getSnapshotBeforeUpdate -> componentDidUpdate -> componentWillUnmount

运行实例：
```
DOM
    真实DOM节点
-------
effect
    每个workInProgress tree节点上都有一个effect list
    用来存放diff结果
    当前节点更新完毕会向上merge effect list（queue收集diff结果）
- - - -
workInProgress
    workInProgress tree是reconcile过程中从fiber tree建立的当前进度快照，用于断点恢复
- - - -
fiber
    fiber tree与vDOM tree类似，用来描述增量更新所需的上下文信息
-------
elements
    描述UI长什么样子（type, props）
```

执行阶段：
React setState 之后，将会运行 differ 算法创建更新，将更新任务推入更新队列。Fiber 负责调度任务，如果有优先级较高的任务插入，将生成 workInProgress tree 保存快照，可以继续执行时则恢复快照继续执行。

```
// 第1阶段 render/reconciliation，可中断
componentWillMount
componentWillReceiveProps
shouldComponentUpdate
componentWillUpdate

// 第2阶段 commit，不可中断
componentDidMount
componentDidUpdate
componentWillUnmount
```

[React 运行过程](https://github.com/coconilu/Blog/issues/99)

## Fiber

React在一些响应体验要求较高的场景不适用，比如动画，布局和手势。根本原因是渲染/更新过程一旦开始无法中断，持续占用主线程，主线程忙于执行 JS，无暇他顾（布局、动画），造成掉帧、延迟响应（甚至无响应）等不佳体验。React Fiber 能够解决主线程长时间占用的问题。Fiber 把渲染/更新过程拆分为小块任务，通过合理的调度机制来控制时间（更细粒度、更强的控制力）。

### 对开发者的影响

* componentWillMount,componentWillReceiveProps,componentWillUpdate几个生命周期方法不再安全，由于任务执行过程可以被打断，这几个生命周期可能会执行多次，如果它们包含副作用(比如Ajax)，会有意想不到的bug。React团队提供了替换的生命周期方法。建议如果使用以上方法，尽量使用纯函数，避免以后踩坑。
* 需要关注react为任务片设置的优先级，特别是页面用动画的情况。避免出现低优先级任务延迟太久执行或永不执行的 bug。优先级大概是：文本框输入 > 本次调度结束需完成的任务 > 动画过渡 > 交互反馈 > 数据更新 > 不会显示但以防将来会显示的任务

[完全理解React Fiber](http://www.ayqy.net/blog/dive-into-react-fiber)

[React Fiber](https://juejin.im/post/5ab7b3a2f265da2378403e57)

[React Fiber是什么](https://zhuanlan.zhihu.com/p/26027085)

## Portal

Portal 提供了一种将子节点渲染到存在于父组件以外的 DOM 节点的优秀的方案。

[React.createPortal 及 Modal 的新实现方式](http://www.ptbird.cn/react-portal-createPortal.html)

## Mixins、HOC、React Hooks

[从Mixins到HOC再到React Hooks](https://juejin.im/post/5d3184596fb9a07eeb13e12c)

## Hooks

### useState

可以用 useEffect 模拟 setState 的回调

### useEffect

* 与 class 组件不同的是，useEffect 允许你把相关的业务逻辑放在一个 effect 函数里，而不是散落在各个生命周期中
* 浅比较，当依赖数组含函数、数组、对象等引用类型时，旧值比对时，总会返回 true。这时需要借助 useCallback 或 useMemo 去缓存旧值。

### useCallback

当需要缓存组件时，配合 React.memo（当 props 改变时才重新渲染）使用

### 更新机制

setXXX 触发组件更新，函数被重新执行，

useRef

## 组件间通信

* 父子间：props
* 子父间：往子组件传回调函数
* 其他：store、context（生成/消费）

## key 的作用

key 是给每一个 vnode 的唯一 id,可以依靠 key,更准确, 更快的拿到 oldVnode 中对应的 vnode 节点，高效和准确的更新节点。
