## 加载原理

webpack 参照 commonJS 规范实现 exports 和 require，然后自动加载入口模块，控制缓存模块。

webpack对于es模块的实现，也是基于自己实现的`__webpack_require__` 和`__webpack_exports__` ，装换成类似于commonjs的形式。对于es模块和commonjs混用的情况，则需要通过`__webpack_require__.n`的形式做一层包装来实现。

webpack通过`__webpack_require__.e`函数实现了动态加载，再通过webpackJsonp函数实现异步加载回调，把模块内容以promise的方式暴露给调用方，从而实现了对code splitting的支持。

[webpack模块化原理-commonjs](https://segmentfault.com/a/1190000010349749)

[webpack模块化原理-ES module](https://segmentfault.com/a/1190000010955254)

[webpack模块化原理-Code Splitting](https://segmentfault.com/a/1190000011435407)