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
　Cat.prototype = new Animal();

　Cat.prototype.constructor = Cat; // 因为上一句更改了 Cat 的 prototype，即 Cat.prototype.constructor 原本执行 Cat 自己，但是被改了。这一句是修正回来。
```

[Javascript继承机制的设计思想](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)

[Javascript面向对象编程（二）：构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html)

[Javascript面向对象编程（三）：非构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html)

### 静态方法、动态方法

静态方法：声明一个仅供当前类或当前类的子类使用的方法。静态的方法在整个应用程序其间存储在内存中，速度快，但占用内存，调用频繁的可以用静态方法。

动态方法：创建实例化对象可直接调用的方法	

[JavaScript中class类的三种方法详解（静态方法、普通方法与构造方法）](https://blog.csdn.net/momDIY/article/details/79997793)
