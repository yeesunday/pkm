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

Map 类似于对象，也是键值对的集合，但是对象的键只能是字符串，Map 的键可以是任意类型。WeakMap 键名同 WeakSet 只能是引用。

[Set、Map、WeakSet 和 WeakMap 的区别](https://juejin.im/post/5d39d14c518825625337f84e)

## Array
Array fill 方法，如果是对象，则填充的是对象的引用。例如
```
  const array = new Array(3).fill([0])
  array[0][0] = 1
  array[1][0] === 1 // true
```

## RegExp

* [Simple Tutorial](http://www.cnblogs.com/onepixel/p/5218904.html)

## JS i18n

* [JavaScript Internationalization API](https://marcoscaceres.github.io/jsi18n/)

## Object.defineProperty

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 相比于点号赋值，`Object.defineProperty` 方法是对属性更加精确的定义。