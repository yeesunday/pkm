## AMD、CMD、CommonJS、ES6 Module

JS 模块化发展：IIFE -> CommonJS -> ES6 Module

1. AMD一开始是CommonJS规范中的一个草案，全称是Asynchronous Module Definition，即异步模块加载机制。后来由该草案的作者以RequireJS实现了AMD规范，所以一般说AMD也是指RequireJS。对于依赖的模块，AMD推崇**依赖前置，提前执行**。也就是说，在define方法里传入的依赖模块(数组)，会在一开始就下载并执行。

2. CMD是SeaJS在推广过程中生产的对模块定义的规范，在Web浏览器端的模块加载器中，SeaJS与RequireJS并称，SeaJS作者为阿里的玉伯。对于依赖的模块，CMD推崇**依赖就近，延迟执行**。也就是说，只有到require时依赖模块才执行。

3. CommonJS规范为CommonJS小组所提出，目的是弥补JavaScript在服务器端缺少模块化机制，NodeJS、webpack都是基于该规范来实现的。webpack 最终编译的结果是符合 CommonJS 规范的 IIFE。关键字`exports`、`require`、`module`、`__filename`、`__dirname`。CommonJS的特点：

  * 所有代码都运行在模块作用域，不会污染全局作用域；
  * 模块是同步加载的，即只有加载完成，才能执行后面的操作；
  * 模块在首次执行后就会缓存，再次加载只返回缓存结果，如果想要再次执行，可清除缓存；
  * CommonJS输出是值的拷贝(即，require返回的值是被输出的值的拷贝，模块内部的变化也不会影响这个值)。

4. ES6 Module是ES6中规定的模块体系，相比上面提到的规范， ES6 Module有更多的优势，有望成为浏览器和服务器通用的模块解决方案。关键字`import`、`export`。ES6 Module的特点(对比CommonJS)

  * CommonJS模块是运行时加载，ES6 Module是编译时输出接口；
  * CommonJS加载的是整个模块，将所有的接口全部加载进来，ES6 Module可以单独加载其中的某个接口；
  * CommonJS输出是值的拷贝，ES6 Module输出的是值的引用，被输出模块的内部的改变会影响引用的改变；
  * CommonJS this指向当前模块，ES6 Module this指向undefined;

[再次梳理AMD、CMD、CommonJS、ES6 Module的区别](https://juejin.im/post/5db95e3a6fb9a020704bcd8d)

[CommonJS 和 ES6 Module 究竟有什么区别？](https://juejin.im/post/5e5f10176fb9a07cd443c1e2)

## 包管理工具

[发展历史](https://segmentfault.com/a/1190000021335004)

[npm scope](https://www.jianshu.com/p/ac5b5f65320b)