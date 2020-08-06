## 宏任务和微任务

JS 执行过程

![](../../assets/js-workflow.png)

1. 所有同步任务都在主线程上执行，形成一个"执行栈"（execution context stack）；
2. 主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件；
3. 一旦"执行栈"中的所有同步任务执行完毕，系统就会取出"任务队列"中事件所对应的回调函数进入"执行栈"，开始执行；
4. 主线程不断重复上面的第三步。

微任务和宏任务皆为异步任务，它们都属于一个队列。宏任务和微任务执行完成后都会判断是否还有微任务，有的话执行微任务，没有就执行宏任务，如此循坏。

常见的宏任务：整体代码 script，setTimeout，setInterval、setImmediate

常见的微任务：原生 Promise(有些实现的promise将then方法放到了宏任务中)、process.nextTick、 MutationObserver

![](../../assets/hongwei.png)

注意：Promise的链式调用then，每次都会在内部生成一个新的Promise，然后执行then，在执行的过程中不断向微任务(microtask)推入新的函数，因此直至微任务(microtask)的队列清空后才会执行下一波的macrotask。例子：

```js
setTimeout(()=>{
   console.log(1) 
},0)
let a=new Promise((resolve)=>{
    console.log(2)
    resolve()
}).then(()=>{
   console.log(3) 
}).then(()=>{
   console.log(4) 
})
console.log(5) 
```

[全方位理解JavaScript的Event Loop](https://juejin.im/post/6844903692898942990)

[JS事件循环机制（event loop）之宏任务/微任务](https://juejin.im/post/5b498d245188251b193d4059)

[微任务、宏任务与Event-Loop](https://juejin.im/post/5b73d7a6518825610072b42b)

[Eventloop不可怕，可怕的是遇上Promise](https://juejin.im/post/6844903808200343559)