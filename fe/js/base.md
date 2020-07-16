## 数据类型

7 种原始类型:
* Boolean
* Null
* Undefined
* Number
* BigInt
* String
* Symbol
和 Object

## 新特性

* [ES6、ES7、ES8、ES9、ES10新特性一览](https://juejin.im/post/5ca2e1935188254416288eb2)

## Set、Map、WeakSet 和 WeakMap 的区别

Set 集合中的元素无序且唯一，集合中的元素可以是任何类型，无论是原始值还是对象引用。WeakSet 只能是引用，所以只要 WeakSet 成员对象在外部消失，它们在 WeakSet 里面的引用就会自动消失。

Map 类似于对象，也是键值对的集合，但是对象的键只能是字符串，Map 的键可以是任意类型，且是有序的。WeakMap 键名同 WeakSet 只能是引用。

[Set、Map、WeakSet 和 WeakMap 的区别](https://juejin.im/post/5d39d14c518825625337f84e)

## Array
Array fill 方法，如果是对象，则填充的是对象的引用。例如
```
  const array = new Array(3).fill([0])
  array[0][0] = 1
  array[1][0] === 1 // true
```

reduce：`arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])`，如果提供了initialValue，则起始索引号为0，否则从索引1起始。

## RegExp

* [Simple Tutorial](http://www.cnblogs.com/onepixel/p/5218904.html)

## JS i18n

* [JavaScript Internationalization API](https://marcoscaceres.github.io/jsi18n/)

## Object.defineProperty

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 相比于点号赋值，`Object.defineProperty` 方法是对属性更加精确的定义。

## 原型和继承

### 原型

![](../../assets/prototype.png)

1. js在创建对象的时候，都有一个叫做 `__proto__` 的内置属性，用于指向创建它的函数对象的原型对象 prototype
2. 只有函数有 prototype, 当你创建一个函数时，js会自动为这个函数加上prototype属性，值是一个空对象
3. Function 和 Object 是两个函数
4. `__proto__` 将实例对象和构造函数原型连接起来组成了原型链，当读取实例的属性时，如果找不到，就会查找与对象关联的原型中的属性，如果还查不到，就去找原型的原型，一直找到最顶层为止。

[JavaScript深入之从原型到原型链](https://github.com/mqyqingfeng/blog/issues/2)

### 继承

在JS中实现继承，大概有两种思路：使用构造函数或使用原型链。但两者各有利弊，构造函数继承会造成资源的浪费，因为每个实例都会创建父类的属性和方法副本；原型链继承当有包含引用类型值的原型时，则容易造成数据上的混乱。实际更多是两者结合形成组合继承。

```
  function Cat() {
    Animal.call(this)
  }

　Cat.prototype = new Animal(); 
　Cat.prototype.constructor = Cat; // 因为上一句更改了 Cat 的 prototype，即 Cat.prototype.constructor 原本执行 Cat 自己，但是被改了。这一句是修正回来。
```

组合继承调用了两次父类的 constructor，寄生式组合继承可以只拷贝父类的 prototype 属性。

```
function Cat() {
  Animal.call(this);
}

Cat.prototype = Object.create(Animal.prototype, {
  constructor: {
    value: Cat
  }
})

// 继承函数
function inherits(ctor, superCtor) {
  ctor.super_ = superCtor;
  ctor.prototype = Object.create(superCtor.prototype, {
    constructor: {
      value: ctor,
      enumerable: false,
      writable: true,
      configurable: true
    }
  });
}; 
function Cat() {
  Animal.call(this);
  //...
}
inherits(Cat, Animal);

Cat.prototype.fun = ...
```

[Javascript继承机制的设计思想](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)

[js继承、构造函数继承、原型链继承、组合继承、组合继承优化、寄生组合继承](https://segmentfault.com/a/1190000015216289)

### 静态方法、动态方法

静态方法：声明一个仅供当前类或当前类的子类使用的方法。静态的方法在整个应用程序其间存储在内存中，速度快，但占用内存，调用频繁的可以用静态方法。

动态方法：创建实例化对象可直接调用的方法	

[JavaScript中class类的三种方法详解（静态方法、普通方法与构造方法）](https://blog.csdn.net/momDIY/article/details/79997793)

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