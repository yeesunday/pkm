## 深拷贝与浅拷贝

浅拷贝是对象的逐位复制。创建一个新对象，该对象具有原始对象中值的精确副本。如果对象的任何字段是对其他对象的引用，则只复制引用地址，即，复制内存地址。大白话讲就是，浅拷贝是对对象地址的复制，并没有开辟新的栈，也就是复制的结果是两个对象指向同一个地址，修改其中一个对象的属性，则另一个对象的属性也会改变。

深拷贝复制所有字段，并复制字段所指向的动态分配内存。深拷贝发生在对象及其引用的对象被复制时。大白话讲就是，深拷贝则是开辟新的栈，两个对象对应两个不同的地址，修改一个对象的属性，不会改变另一个对象的属性。

```
浅拷贝
function shallowClone(obj){
    var newObj={};
    for (var key in obj){
        newObj[key]=obj[key]
    }
    return newObj;
}

深拷贝
function deepClone(obj) {
    if (obj === null) return null; //null 的情况
    if (obj instanceof RegExp) return new RegExp(obj); //正则表达式的情况
    if (obj instanceof Date) return new Date(obj); //日期对象的情况
    if (typeof obj == 'Function') return new function(obj){}; //函数的情况
    if (typeof obj != "object") {
    //非复杂类型,直接返回 也是结束递归的条件
    return obj
    }
    //[].__proto__.constructor=Array()
    //{}.__proto__.constructor=Object()
    //因此处理数组的情况时,可以取巧用这个办法来new新对象
    var newObj = new obj.__proto__.constructor;
    for (var key in obj) {
    newObj[key] = deepClone(obj[key])
    }
    return newObj;
}
```
[原生js实现深拷贝](https://juejin.im/post/5da47110f265da5b633cdf2f)

## 防抖和节流

对于高频调用，降低执行频率。一般使用形式为抛出一个闭包函数，用 setTimeout、调用判断和 `apply` (把上下文还原)实现。防抖适用于`延后执行`，节流适用于`限制频率`。

防抖：触发高频事件后n秒内函数只会执行一次，如果n秒内高频事件再次被触发，则重新计算时间。思路为每次触发事件时都取消之前的延时调用方法。
```
function debounce(fn, wait, immediate) {
    var timer = null;
    return function() {
        var context = this;
        var args = arguments;

        // 判断首次是否需要立即执行
        if (immediate) {
            fn.call(context, ...args);
            immediate = false;
        }

        // 清除定时器
        clearTimeout(timer);
        timer = setTimeout(function() {
            fn.call(context, ...args);
        }, wait);
    };
}
```

节流：高频事件触发，但在n秒内只会执行一次，所以节流会稀释函数的执行频率。思路为每次触发事件时都判断当前是否有等待执行的延时函数。
```
function throttle(fn, wait, immediate) {
    var timer = null;
    return function() {
        var context = this;
        var args = arguments;

        // 判断首次是否需要立即执行
        if (immediate) {
            fn.call(context, ...args);
            immediate = false;
        }

        // 如果当前存在定时器，返回；否则设置定时器
        if (timer) return;

        timer = setTimeout(function() {
            fn.call(context, ...args);
            // 函数执行完毕后，清除定时器
            clearTimeout(timer);
            timer = null;
        }, wait);
    };
}
```

[什么是防抖和节流？有什么区别？如何实现？](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/5)

## 函数组合

compose(f1, f2, f3) -> f3(f2(f1()))

```
<!-- 啰嗦版 -->
const compose = function(...args) {
  let result
  return function(...arg2) {
    result = args[0](...arg2)
    for(i = 1, l = args.length; i < l; i++) {
      result = args[i](result)
    }
    return result
  }
}

<!-- 炫酷版 -->
const compose = (...args) => (...arg2) => args.reduce((r, f, index) => index === 0 ? f(...r) : f(r), arg2)
```