## 扁平化

```js
function flatten(arr) {
    return arr.reduce((acc, cur) => acc.concat(Array.isArray(cur) ? flatten(cur) : cur), [])
}
// 指定深度
function flatten(arr, deep) {
    return arr.reduce((acc, cur) => acc.concat(Array.isArray(cur) && deep > 1 ? flatten(cur, deep - 1) : cur), [])
}
```

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

对于高频调用，降低执行频率。一般使用形式为抛出一个闭包函数，注意上下文应用和参数透传。防抖适用于`延后执行`，节流适用于`限制频率`。

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
function compose(...funcs) {
  return funcs.reduce((a, b) => (...args) => a(b(...args)))
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

## JSONP

```javascript
(function (window,document) {
    "use strict";
    var jsonp = function (url,data,callback) {

        // 1.将传入的data数据转化为url字符串形式
        // {id:1,name:'jack'} => id=1&name=jack
        var dataString = url.indexof('?') == -1? '?': '&';
        for(var key in data){
            dataString += key + '=' + data[key] + '&';
        };

        // 2 处理url中的回调函数
        // cbFuncName回调函数的名字 ：my_json_cb_名字的前缀 + 随机数（把小数点去掉）
        var cbFuncName = 'my_json_cb_' + Math.random().toString().replace('.','');
        dataString += 'callback=' + cbFuncName;

        // 3.创建一个script标签并插入到页面中
        var scriptEle = document.createElement('script');
        scriptEle.src = url + dataString;

        // 4.挂载回调函数
        window[cbFuncName] = function (data) {
            callback(data);
            // 处理完回调函数的数据之后，删除jsonp的script标签
            document.body.removeChild(scriptEle);
        }

        document.body.appendChild(scriptEle);
    }

    window.$jsonp = jsonp;

})(window,document)
```

## 私有变量实现

```js
// 闭包
class Example {
  constructor() {
    var _private = '';
    _private = 'private';
    this.getName = function() {return _private}
  }
}

var ex = new Example();

console.log(ex.getName()); // private
console.log(ex._private); // undefined

```

[ES6 系列之私有变量的实现](https://juejin.im/post/6844903717561434126)

## 异步编程方案

1. 回调函数
2. 事件监听
3. 发布订阅
4. promise
5. async / await
6. Generators/ yield

[JS 异步编程六种方案](https://juejin.im/post/6844903760280420366)