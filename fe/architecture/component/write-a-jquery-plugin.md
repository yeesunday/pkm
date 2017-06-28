jQuery插件有哪几种类型？
封装对象方法的插件（对象级别）
这类插件是最常见的一种，即将对象方法进行封装，然后通过选择器获取的jQuery对象进行操作。
用法：$('#id').myPlugin()。
封装全局函数的插件（类级别）
即将独立的函数加到jquery命名空间下, 拓展jQuery类，典型例子$.ajax()
用法：$.myPlugin()
$.extend方法和$.fn.extend方法都可以用来扩展jQuery功能，通过阅读jQuery源码我们可以发现这两个方法的本质区别，那就是$.extend方法是在jQuery全局对象上扩展方法，$.fn.extend方法是在$选择符选择的jQuery对象上扩展方法。所以扩展jQuery的公共方法一般用$.extend方法，定义插件一般用$.fn.extend方法。


jQuery.fn=jQuery.prototype，也就是说jQuery.fn对象是jQuery的原型对象,jQuery的DOM操作方法都在jQuery.fn对象上定义的，然后jQuery对象就可以通过原型继承这些方法。

链式调用

防止$符号污染的jQuery插件

jQuery.noConflict()方法交出$符号的使用权

可以接受参数的jQuery插件


资料参考：
* http://www.jianshu.com/p/518d424d4994
* https://gist.github.com/quexer/3619237



