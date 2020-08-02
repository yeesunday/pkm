## web 语义化

* 正确的标签做正确的事情
* 页面内容结构化
* 无CSS样子时也容易阅读，便于阅读维护和理解
* 便于浏览器、搜索引擎解析。 利于爬虫标记、利于SEO

html语义化标签包括 body, article, nav, aside, section, header, footer, hgroup, 还有 h1-h6 address等。

[快速理解web语义化](https://juejin.im/entry/6844903582274174984)

## 伪类/伪元素

伪类用于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的。比如:hover

伪元素用于创建一些不在文档树中的元素，并为其添加样式。比如::before 一般建议使用双冒号表示。

[总结伪类与伪元素](http://www.alloyteam.com/2016/05/summary-of-pseudo-classes-and-pseudo-elements/)

## disabled 和 readonly 的区别

这两种写法都会使显示出来的文本框不能输入文字，都能做到使用户不能够更改表单域中的内容，但：

1. disabled 会使文本框变灰，而 readonly 只是使文本框不能输入，外观没有变化。
2. readonly 只针对 input 和 textarea 有效，而 disabled 对于所有的表单元素都有效。
3. 将表单以 POST 或 GET 的方式提交的话，使用了 disabled 后，这个元素的值不会被传递出去，而 readonly 会将该值传递出去。

