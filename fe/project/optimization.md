## 常见的 Web 性能优化方案

1. 请求数量——合并脚本和样式表，CSS Sprites，按需加载
2. 请求带宽——开启Gzip，精简JavaScript，移除重复脚本，图像优化
3. 缓存利用——使用CDN，使用外部JavaScript和CSS，使用浏览器缓存，预解析DNS
4. 页面结构——将样式表放在顶部，将脚本放在底部，尽早刷新文档的输出
5. 代码校验——避免CSS表达式，防抖节流，尽可能减少 dom 操作
6. 减少握手次数——避免重定向，[KeepAlive](https://www.cnblogs.com/sunhk/p/5182054.html)

## CSS3 开启 GPU 硬件加速

CSS animations, transforms 以及 transitions 不会自动开启GPU加速，而是由浏览器的缓慢的软件渲染引擎来执行。那我们怎样才可以切换到GPU模式呢，很多浏览器提供了某些触发的CSS规则。现在，像Chrome, FireFox, Safari, IE9+和最新版本的Opera都支持硬件加速，当它们检测到页面中某个DOM元素应用了某些CSS规则时就会开启，最显著的特征的元素的3D变换。例如：

```
.cube {
   transform: translate3d(250px,250px,250px)
   rotate3d(250px,250px,250px,-120deg)
   scale3d(0.5, 0.5, 0.5);
   transform: translateZ(0);
}
```

[用CSS开启硬件加速来提高网站性能](https://www.cnblogs.com/rubylouvre/p/3471490.html)