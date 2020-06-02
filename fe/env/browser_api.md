## DOM 和 BOM

DOM（document object model）：文档对象模型，提供操作页面元素的方法和属性

BOM（browser object model）；浏览器对象模型，提供一些属性和方法可以操作浏览器

[最全的DOM和BOM的解释分析](https://juejin.im/post/5d7677b06fb9a06afd662d20)

## 存储机制

| 特性	| Cookie | localStorage | sessionStorage |
|  ----  | ----  | ----  | ----  |
| 数据的生命期	| 一般由服务器生成，可设置失效时间。如果在浏览器端生成Cookie，默认是关闭浏览器后失效	| 除非被清除，否则永久保存	| 仅在当前会话下有效，关闭页面或浏览器后被清除 |
| 存放数据大小	| 4K左右	| 一般为5MB | 一般为5MB |
| 与服务器端通信	| 每次都会携带在HTTP头中，如果使用cookie保存过多数据会带来性能问题	| 仅在客户端（即浏览器）中保存，不参与和服务器的通信 | 仅在客户端（即浏览器）中保存，不参与和服务器的通信 |
| 易用性	| 需要程序员自己封装，源生的Cookie接口不友好	| 源生接口可以接受，亦可再次封装来对Object和Array有更好的支持 | 源生接口可以接受，亦可再次封装来对Object和Array有更好的支持 |

[详解 Cookie，Session，Token](https://juejin.im/post/5d01f82cf265da1b67210869)

### 单点登录的实现

使用 token，成熟方案是 JWT（JSON Web Token），解决 session 无法共享登录状态到子系统的问题。

![](../../assets/sso.png)