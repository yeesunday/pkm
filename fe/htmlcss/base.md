## web 语义化

* 正确的标签做正确的事情
* 页面内容结构化
* 无CSS样子时也容易阅读，便于阅读维护和理解
* 便于浏览器、搜索引擎解析。 利于爬虫标记、利于SEO

html语义化标签包括 body, article, nav, aside, section, header, footer, hgroup, 还有 h1-h6 address等。

[快速理解web语义化](https://juejin.im/entry/6844903582274174984)

## DOM 事件流

先捕获再冒泡

* addEventListener的第三个参数默认为false，为 true 时在捕获时触发。`element.addEventListener(event, function, useCapture)`
* e.stopPropagation()：既可以阻止事件冒泡，也可以阻止事件捕获，也可以阻止处于目标阶段。兼容 ie 写法 `window.event.cancelBubble = true; `
* e.preventDefault()：取消默认事件

### 事件委托

优点：
1. 减少事件注册，节省内存
2. 减少了dom节点更新的操作，处理逻辑只需在委托元素上进行。如：新添加的li不用绑定事件，删除li时，不需要进行元素与处理函数的解绑。

缺点：
1. 事件委托基于冒泡，对于onfoucs和onblur等事件不支持
2. 层级过多，冒泡过程中，可能会被某层 event.stopPropagation 等阻止掉（建议就近委托）




