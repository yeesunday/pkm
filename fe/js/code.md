## 函数柯里化

在数学和计算机科学中，柯里化是一种将使用多个参数的一个函数转换成一系列使用一个参数的函数的技术。实现：

1. 判断当前函数传入的参数是否大于或等于fn需要参数的数量，如果是，直接执行fn。
2. 如果传入参数数量不够，返回一个闭包，暂存传入的参数，并重新返回 currying 函数

```
function currying(fn, ...args) {
    if (args.length >= fn.length) {
        return fn(...args);
    } else {
        return (...args2) => currying(fn, ...args, ...args2);
    }
}
```


## 防抖和节流

对于高频调用，降低执行频率。一般使用形式为抛出一个闭包函数，用 setTimeout、调用判断和 `apply` (把上下文还原)实现。防抖适用于`延后执行`，节流适用于`限制频率`。

防抖：触发高频事件后 n 秒内函数只会执行一次，如果 n 秒内高频事件再次被触发，则重新计算时间。思路为每次触发事件时都取消之前的延时调用方法。

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

节流：高频事件触发，但在 n 秒内只会执行一次，所以节流会稀释函数的执行频率。思路为每次触发事件时都判断当前是否有等待执行的延时函数。

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

## Call，Apply，Bind 的使用与区别

相同点:

- 都是使用于方法借用及明确 this 指向场景
- 第一个参数都是 this 要指向的对象
- 都可以利用后续参数传参

不同点:

- 参数传递方式不同
- call,apply 是立即调用,bind 是动态调用

基本使用:

- Array.prototype.slice.call(obj,0,1,2)
- Array.prototype.slice.apply(obj,[0,1,2])
- Array.prototype.slice.bind(obj)(0,1,2)

从上面的例子可以看出来 call,apply 使用上几乎保持一致，而 bind 实际上是返回了一个函数

```
// call
Function.prototype.myCall = function (context = window, ...args) {
    if (this === Function.prototype) {
    return undefined; // 用于防止 Function.prototype.myCall() 直接调用
    }
    context = context || window;
    const fn = Symbol();
    context[fn] = this;
    const result = context[fn](...args);
    delete context[fn];
    return result;
}

// apply
Function.prototype.myApply = function (context = window, args) {
    if (this === Function.prototype) {
    return undefined; // 用于防止 Function.prototype.myCall() 直接调用
    }
    const fn = Symbol();
    context[fn] = this;
    let result;
    if (Array.isArray(args)) {
    result = context[fn](...args);
    } else {
    result = context[fn]();
    }
    delete context[fn];
    return result;
}

// bind
Function.prototype.myBind = function (context,...args1) {
    if (this === Function.prototype) {
    throw new TypeError('Error')
    }
    const _this = this
    return function F(...args2) {
    // 判断是否用于构造函数
    if (this instanceof F) {
        return new _this(...args1, ...args2)
    }
    return _this.apply(context, args1.concat(args2))
    }
}
```

## 深拷贝与浅拷贝

浅拷贝是对象的逐位复制。创建一个新对象，该对象具有原始对象中值的精确副本。如果对象的任何字段是对其他对象的引用，则只复制引用地址，即，复制内存地址。大白话讲就是，浅拷贝是对对象地址的复制，并没有开辟新的栈，也就是复制的结果是两个对象指向同一个地址，修改其中一个对象的属性，则另一个对象的属性也会改变。

深拷贝复制所有字段，并复制字段所指向的动态分配内存。深拷贝发生在对象及其引用的对象被复制时。大白话讲就是，深拷贝则是开辟新的栈，两个对象对应两个不同的地址，修改一个对象的属性，不会改变另一个对象的属性。

```
// 浅拷贝
function shallowClone(obj){
    var newObj={};
    for (var key in obj){
        newObj[key]=obj[key]
    }
    return newObj;
}

// 深拷贝
const mapTag = '[object Map]';
const setTag = '[object Set]';
const arrayTag = '[object Array]';
const objectTag = '[object Object]';
const argsTag = '[object Arguments]';

const boolTag = '[object Boolean]';
const dateTag = '[object Date]';
const numberTag = '[object Number]';
const stringTag = '[object String]';
const symbolTag = '[object Symbol]';
const errorTag = '[object Error]';
const regexpTag = '[object RegExp]';
const funcTag = '[object Function]';

const deepTag = [mapTag, setTag, arrayTag, objectTag, argsTag];


function forEach(array, iteratee) {
    let index = -1;
    const length = array.length;
    while (++index < length) {
        iteratee(array[index], index);
    }
    return array;
}

function isObject(target) {
    const type = typeof target;
    return target !== null && (type === 'object' || type === 'function');
}

function getType(target) {
    return Object.prototype.toString.call(target);
}

function getInit(target) {
    const Ctor = target.constructor;
    return new Ctor();
}

function cloneSymbol(targe) {
    return Object(Symbol.prototype.valueOf.call(targe));
}

function cloneReg(targe) {
    const reFlags = /\w*$/;
    const result = new targe.constructor(targe.source, reFlags.exec(targe));
    result.lastIndex = targe.lastIndex;
    return result;
}

function cloneFunction(func) {
    const bodyReg = /(?<={)(.|\n)+(?=})/m;
    const paramReg = /(?<=\().+(?=\)\s+{)/;
    const funcString = func.toString();
    if (func.prototype) {
        const param = paramReg.exec(funcString);
        const body = bodyReg.exec(funcString);
        if (body) {
            if (param) {
                const paramArr = param[0].split(',');
                return new Function(...paramArr, body[0]);
            } else {
                return new Function(body[0]);
            }
        } else {
            return null;
        }
    } else {
        return eval(funcString);
    }
}

function cloneOtherType(targe, type) {
    const Ctor = targe.constructor;
    switch (type) {
        case boolTag:
        case numberTag:
        case stringTag:
        case errorTag:
        case dateTag:
            return new Ctor(targe);
        case regexpTag:
            return cloneReg(targe);
        case symbolTag:
            return cloneSymbol(targe);
        case funcTag:
            return cloneFunction(targe);
        default:
            return null;
    }
}

function clone(target, map = new WeakMap()) {

    // 克隆原始类型
    if (!isObject(target)) {
        return target;
    }

    // 初始化
    const type = getType(target);
    let cloneTarget;
    if (deepTag.includes(type)) {
        cloneTarget = getInit(target, type);
    } else {
        return cloneOtherType(target, type);
    }

    // 防止循环引用
    if (map.get(target)) {
        return target;
    }
    map.set(target, cloneTarget);

    // 克隆set
    if (type === setTag) {
        target.forEach(value => {
            cloneTarget.add(clone(value));
        });
        return cloneTarget;
    }

    // 克隆map
    if (type === mapTag) {
        target.forEach((value, key) => {
            cloneTarget.set(key, clone(value));
        });
        return cloneTarget;
    }

    // 克隆对象和数组
    const keys = type === arrayTag ? undefined : Object.keys(target);
    forEach(keys || target, (value, key) => {
        if (keys) {
            key = value;
        }
        cloneTarget[key] = clone(target[key], map);
    });

    return cloneTarget;
}
```

[原生 js 实现深拷贝](https://juejin.im/post/5da47110f265da5b633cdf2f)