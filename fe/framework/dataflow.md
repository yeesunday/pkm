根据「隔离变化」和「约定优于配置」的思想，把组件之间需要共享的状态抽取出来，遵循特定的约定，统一来管理，让状态的变化可以预测。根据这个思路，产生了很多的模式和库。

Redux 有三大原则：
1. 单一数据源：Flux 的数据源可以是多个。 
2. State 是只读的：Flux 的 State 可以随便改。 
3. 使用纯函数来执行修改：Flux 执行修改的不一定是纯函数。

Flux 和 Redux 都是**单向数据流**

[Vuex、Flux、Redux、Redux-saga、Dva、MobX](https://zhuanlan.zhihu.com/p/53599723)

[浅析redux-saga中间件及用法](http://blog.poetries.top/2018/08/29/redux-saga-and-redux-thunk/)