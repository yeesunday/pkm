## 常见的 Web 性能优化方案

1. 请求数量——合并脚本和样式表，CSS Sprites，按需加载
2. 请求带宽——开启Gzip，精简JavaScript，移除重复脚本，图像优化
3. 缓存利用——使用CDN，使用外部JavaScript和CSS，使用浏览器缓存，预解析DNS
4. 页面结构——将样式表放在顶部，将脚本放在底部，尽早刷新文档的输出
5. 代码校验——避免CSS表达式，防抖节流，尽可能减少 dom 操作
6. 减少握手次数——避免重定向，[KeepAlive](https://www.cnblogs.com/sunhk/p/5182054.html)