## Promise

[可能是目前最易理解的手写promise](https://juejin.im/post/5dc383bdf265da4d2d1f6b23)

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

```js
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