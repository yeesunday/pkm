## disabled 和 readonly 的区别

这两种写法都会使显示出来的文本框不能输入文字，都能做到使用户不能够更改表单域中的内容，但：

1. disabled 会使文本框变灰，而 readonly 只是使文本框不能输入，外观没有变化。
2. readonly 只针对 input 和 textarea 有效，而 disabled 对于所有的表单元素都有效。
3. 将表单以 POST 或 GET 的方式提交的话，使用了 disabled 后，这个元素的值不会被传递出去，而 readonly 会将该值传递出去。