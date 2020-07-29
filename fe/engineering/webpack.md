## tree-shaking

Tree-shaking的本质是消除无用的js代码。无用代码消除在广泛存在于传统的编程语言编译器中，编译器可以判断出某些代码根本不影响输出，然后消除这些代码，这个称之为DCE（dead code elimination）。

副作用意思是一个函数会、或者可能会对函数外部变量产生影响的行为。

生产环境源码一般要经过 babel 编译，但编译后，全部模块被封装成 IIFE。因为IIFE比较特殊，它在被翻译时(JS并非编译型的语言)就会被执行，Webpack不做程序流分析，它不知道IIFE会做什么特别的事情，所以不会删除这部分代码。而 rollup 做了程序流分析，会删除 IIFE 里没有副作用的代码。webpack 的 shaking 是模块级别的，而 rollup 可以做到语句级别。如果需要 webpack 对某个含有副作用代码的模块进行 shaking，可以设置 `sideEffects: false`

[你的Tree-Shaking并没什么卵用](https://juejin.im/post/5a5652d8f265da3e497ff3de)

[Webpack Tree shaking 深入探究](https://juejin.im/post/5bb8ef58f265da0a972e3434)

## 加载原理

webpack 参照 commonJS 规范实现 exports 和 require，然后自动加载入口模块，控制缓存模块。

webpack对于es模块的实现，也是基于自己实现的`__webpack_require__` 和`__webpack_exports__` ，装换成类似于commonjs的形式。对于es模块和commonjs混用的情况，则需要通过`__webpack_require__.n`的形式做一层包装来实现。

webpack通过`__webpack_require__.e`函数实现了动态加载，再通过webpackJsonp函数实现异步加载回调，把模块内容以promise的方式暴露给调用方，从而实现了对code splitting的支持。

[webpack模块化原理-commonjs](https://segmentfault.com/a/1190000010349749)

[webpack模块化原理-ES module](https://segmentfault.com/a/1190000010955254)

[webpack模块化原理-Code Splitting](https://segmentfault.com/a/1190000011435407)

## 性能优化

1. 提高打包速度
  * 缩小文件的搜索范围，关键字`resolve` `noParse` `include` `exclude`
  * 减少基础模块的编译次数，关键字 `DllPlugin`
  * 多线程编译，关键字 `happypack`
2. 减小打包体积
  * 压缩文件，关键字 `UglifyJS` 
  * 剔除死代码，关键字 `Tree Shaking`
3. 按需加载，关键字 `Code Splitting`

[三十分钟掌握Webpack性能优化](https://juejin.im/post/5b652b036fb9a04fa01d616b)

## 编写插件

插件是由一个构造函数（此构造函数上的 prototype 对象具有 apply 方法）的所实例化出来的。这个 apply 方法在安装插件时，会被 webpack compiler 调用一次。apply 方法可以接收一个 webpack compiler 对象的引用，从而可以在回调函数中访问到 compiler 对象。插件就是在 compiler 对象的钩子回调里做逻辑操作。

[webpack 文档-编写一个插件](https://webpack.docschina.org/contribute/writing-a-plugin/)

## HMR

Hot Module Replacement，简称HMR，无需完全刷新整个页面的同时，更新模块。HMR的好处，在日常开发工作中体会颇深：节省宝贵的开发时间、提升开发体验。HMR 与 live reload 是两个不同的概念。

1. webpack-dev-server 监听文件系统变化，变化时，重新编译到内存中
2. 通过 websocket，服务器推送给浏览器新模块的 hash 值
3. 通过 websocket，服务器推送给浏览器新模块处于 ok 状态
4. 处于浏览器的 webpack 客户端向服务器发起 jsonp 请求，拿回新模块代码
5. 删除新模块，添加新模块，通过__webpack_require__执行相关模块的代码，完成模块的更新

[Webpack HMR 原理解析](https://zhuanlan.zhihu.com/p/30669007)

[轻松理解webpack热更新原理](https://juejin.im/post/5de0cfe46fb9a071665d3df0)