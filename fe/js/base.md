## 数据类型

7 种基本类型，栈存值
* Boolean
* Null
* Undefined
* Number
* BigInt
* String
* Symbol

5 种引用类型，堆存值，栈存引用
* Object
* Array
* Date
* RegExp
* Function

const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针，const只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它指向的数据结构是不是可变的，就完全不能控制了。因此，将一个对象声明为常量必须非常小心。

```js
const foo = {};
foo.name = "dd";
console.log(foo.name); // 打印"dd"
```


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

## 正则表达式

常用正则

``` js
// 电话
/^1[345789]{1}\d{9}$/
// HEX 颜色值
/(#[A-Fa-f0-9]{6}|#[A-Fa-f0-9]{3})/g
// rgb
/rgb\((\d{1,3}), (\d{1,3}), (\d{1,3})\)/g
```

* [简单教程](http://www.cnblogs.com/onepixel/p/5218904.html)

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
4. `__proto__` 将实例对象和构造函数原型连接起来组成了原型链，当读取实例的属性时，如果找不到，就会查找与对象关联的原型中的属性，如果还查不到，就去找原型的原型，一直找到最顶层为止。构造函数的原型对象呗。构造函数Foo()除了是方法，也是对象，它也有__proto__属性，指向函数的构造函数也就是 Function 的 prototype。

继承意味着复制操作，然而 JavaScript 默认并不会复制对象的属性，相反，JavaScript 只是在两个对象之间创建一个关联，这样，一个对象就可以通过委托访问另一个对象的属性和函数，所以与其叫继承，委托的说法反而更准确些。

[JavaScript深入之从原型到原型链](https://github.com/mqyqingfeng/blog/issues/2)
[js中__proto__和prototype的区别和关系](https://www.zhihu.com/question/34183746)

### 继承

在JS中实现继承，大概有两种思路：使用构造函数或使用原型链。但两者各有利弊，构造函数继承会造成资源的浪费，因为每个实例都会创建父类的属性和方法副本；原型链继承当有包含引用类型值的原型时，则容易造成数据上的混乱。实际更多是两者结合形成组合继承。

```js
  function Cat() {
    Animal.call(this)
  }

　Cat.prototype = new Animal(); 
　Cat.prototype.constructor = Cat; // 因为上一句更改了 Cat 的 prototype，即 Cat.prototype.constructor 原本执行 Cat 自己，但是被改了。这一句是修正回来。
```

组合继承调用了两次父类的 constructor，寄生式组合继承可以只拷贝父类的 prototype 属性。

```js
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

### ES6 继承

```js
class A {
  constructor() {
    this.a = 'hello';
  }
}

class B extends A {
  constructor() {
	super();
	this.b = 'world';
  }
}

let b = new B();
```

与 ES5 的区别在于

1. ES6 子类可以直接通过 `__proto__` 寻址到父类。`Sub.__proto__ === Super;` 而 ES5 不行 `Sub.__proto__ === Function.prototype`
2. ES5 和 ES6 子类 this 生成顺序不同。ES5 的继承先生成了子类实例，再调用父类的构造函数修饰子类实例，ES6 的继承先生成父类实例，再调用子类的构造函数修饰父类实例。这个差别使得 ES6 可以继承内置对象。
3. 类继承是单一继承结构，只有一个父类；而原型继承本质上是组合，它可以有多个父类，且不会产生层级分类这样的副作用。

[ES5/ES6 的继承除了写法以外还有什么区别](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/20)

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

## 闭包

闭包是有权限访问其他函数作用域内的变量的一个函数。

由于闭包可以缓存上级作用域，那么就使得函数外部打破了“函数作用域”的束缚，可以访问函数内部的变量。闭包通常用来创建内部变量，使得这些变量不能被外部随意修改，同时又可以通过指定的函数接口来操作。

应用

* 私有变量
* 防抖节流
* 单例模式实现
* IIFE

PS：内存泄漏（Memory Leak）是指程序中己动态分配的堆内存由于某种原因程序未释放或无法释放，造成系统内存的浪费，导致程序运行速度减慢甚至系统崩溃等严重后果。可以借助 chrome 控制台的 performance 和 memory 工具可以排查内存泄露。

[记录一次前端内存泄漏排查经历](https://juejin.im/post/5df33d97518825126e639c60)


## new 操作符

```js
function New() {
  // 获取构造函数
  Constructor = [].shift.call(arguments)
  // 复制原型
  var obj = Object.create(Constructor.prototype)
  // 复制方法属性
  var result = Constructor.apply(obj, arguments)
  // 如果构造函数返回了对象，则赋值对象
  return typeof result === 'object' ? result || obj : obj
}
var person = New(Person, '小明', 25)
```

1. 获取实参中的第一个参数（构造函数），就是调用New函数传进来的第一个参数，暂时记为Constructor；
2. 使用Constructor的原型链结合Object.create来创建一个对象，此时新对象的原型链为Constructor函数的原型对象；（结合我们上面讨论的，要访问原型链上面的属性和方法，要使用实例对象的__proto__属性）
3. 改变Constructor函数的this指向，指向新创建的实例对象，然后call方法再调用Constructor函数，为新对象赋予属性和方法；（结合我们上面讨论的，要访问构造函数的属性和方法，要使用call或apply）
4. 返回新创建的对象，为Constructor函数的一个实例对象。

## this 指向

this 指向调用它的对象

1. 普通函数指向函数的调用者：有个简便的方法就是看函数前面有没有点,如果有点,那么就指向点前面的那个值;
2. 箭头函数指向函数所在的所用域: 注意理解作用域,只有函数的{}构成作用域,对象的{}以及 if(){}都不构成作用域;

```js
let foo = {
  baz: function() {
  console.log(this);
  }
}

foo.baz();   // 'this' 引用 'foo', 因为 'baz' 被
             // 对象 'foo' 调用

let bar = foo.baz;

bar();       // 'this' 指向全局 window 对象，因为
             // 没有指定引用对象

```

[两句话理解js中的this](https://juejin.im/post/6844903511868571656)

## 上下文

简而言之，执行上下文是评估和执行 JavaScript 代码的环境的抽象概念。每当 Javascript 代码在运行的时候，它都是在执行上下文中运行。

JavaScript 中有三种执行上下文类型。

* 全局执行上下文 — 这是默认或者说基础的上下文，任何不在函数内部的代码都在全局上下文中。它会执行两件事：创建一个全局的 window 对象（浏览器的情况下），并且设置 this 的值等于这个全局对象。一个程序中只会有一个全局执行上下文。
* 函数执行上下文 — 每当一个函数被调用时, 都会为该函数创建一个新的上下文。每个函数都有它自己的执行上下文，不过是在函数被调用时创建的。函数上下文可以有任意多个。每当一个新的执行上下文被创建，它会按定义的顺序（将在后文讨论）执行一系列步骤。
* 块级作用域：{...} 大括号内的代码块，我们称之为一个块级

变量提升：JavaScript 中，函数及变量的声明都将被提升到函数的最顶部。__但初始化不会提升。__

[JavaScript进阶-执行上下文(理解执行上下文一篇就够了)](https://juejin.im/post/6844903983438381069)