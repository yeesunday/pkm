## tree-shaking

Tree-shaking的本质是消除无用的js代码。无用代码消除在广泛存在于传统的编程语言编译器中，编译器可以判断出某些代码根本不影响输出，然后消除这些代码，这个称之为DCE（dead code elimination）。

副作用意思是一个函数会、或者可能会对函数外部变量产生影响的行为。

生产环境源码一般要经过 babel 编译，但编译后，全部模块被封装成 IIFE。因为IIFE比较特殊，它在被翻译时(JS并非编译型的语言)就会被执行，Webpack不做程序流分析，它不知道IIFE会做什么特别的事情，所以不会删除这部分代码。而 rollup 做了程序流分析，会删除 IIFE 里没有副作用的代码。webpack 的 shaking 是模块级别的，而 rollup 可以做到语句级别。如果需要 webpack 对某个含有副作用代码的模块进行 shaking，可以设置 `sideEffects: false`

[你的Tree-Shaking并没什么卵用](https://juejin.im/post/5a5652d8f265da3e497ff3de)

[Webpack Tree shaking 深入探究](https://juejin.im/post/5bb8ef58f265da0a972e3434)

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