根据「隔离变化」和「约定优于配置」的思想，把组件之间需要共享的状态抽取出来，遵循特定的约定，统一来管理，让状态的变化可以预测。根据这个思路，产生了很多的模式和库。

Redux 有三大原则：
1. 单一数据源：Flux 的数据源可以是多个。 
2. State 是只读的：Flux 的 State 可以随便改。 
3. 使用纯函数来执行修改：Flux 执行修改的不一定是纯函数。

Flux 和 Redux 都是**单向数据流**

[大白话解析 Redux 、 redux-thunk 、redux-saga 和 react-redux](https://github.com/lulujianglab/blog/issues/34)

[Vuex、Flux、Redux、Redux-saga、Dva、MobX](https://zhuanlan.zhihu.com/p/53599723)

[浅析redux-saga中间件及用法](http://blog.poetries.top/2018/08/29/redux-saga-and-redux-thunk/)

## redux-thunk

redux-thunk 对 dispatch 方法做了一个升级，如果给 dispatch 传递的仍然是个对象, dispatch 就会把这个对象传给 store ,跟之前的方法没有任何区别；但是假如传的是个函数，就不会直接传递给 store 了，会让这个函数先执行，然后执行完之后需要调用 store ,这个函数再去调用 store。从而实现异步代码拆分。

## redux-saga

当 action 被派发，不仅 reducer 能接收到，saga 也能接收到。saga 接管了异步 action 的处理，使用封装的 API，put 等对 store 进行修改。