## 常见的 Web 性能优化方案

### 工程方面

1. 请求数量——合并脚本和样式表，CSS Sprites，按需加载
2. 请求带宽——开启Gzip，精简JavaScript，移除重复脚本，图像优化
3. 缓存利用——使用CDN，使用外部JavaScript和CSS，使用浏览器缓存，预解析DNS
4. 页面结构——将样式表放在顶部，将脚本放在底部，尽早刷新文档的输出
5. 减少握手次数——避免重定向，[KeepAlive](https://www.cnblogs.com/sunhk/p/5182054.html)

### 语言方面（react）

* 函数式组件 React.memo；类组件 React.PureComponent
* useMemo
* useEffect 或 shouldComponentUpdate
* 避免使用内联对象
* 避免使用匿名函数
* 调整CSS而不是强制组件加载和卸载
* 使用React.Fragment避免添加额外的DOM
* props和state的数据尽可能简单明了，扁平化
* map里面添加key，并且key不要使用index（可变的）

## 首屏优化

1. SSR
2. 骨架屏
3. 加载动画

[一种自动化生成骨架屏的方案](https://github.com/Jocs/jocs.github.io/issues/22)

## 渐进增强和优雅降级

渐进增强：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。

优雅降级：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。

```css
.transition { /*渐进增强写法*/
  -webkit-transition: all .5s;
     -moz-transition: all .5s;
       -o-transition: all .5s;
          transition: all .5s;
}
.transition { /*优雅降级写法*/
          transition: all .5s;
       -o-transition: all .5s;
     -moz-transition: all .5s;
  -webkit-transition: all .5s;
}
```

如何选择：

* 如果低版本用户居多，当然优先采用渐进增强的开发流程；
* 如果高版本用户居多，为了提高大多数用户的使用体验，那当然优先采用优雅降级的开发流程。
* 差不多就用渐进增强，业务可用性是第一

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