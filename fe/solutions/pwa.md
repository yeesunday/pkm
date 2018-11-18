PWA（Progressive Web App）是前端的大趋势，它能极大的加快前端页面的加载速度，得到近乎原生 app 的展示效果（其实难说）。PWA 其实是多种前端技术的组合。

* ​Workbox - Registers a service worker for offline caching.
* ​Manifest - Automatically generate manifest.json file.
* Meta - Automatically adds SEO friendly meta data with manifest integration.
* ​Icon - Automatically generates app icons with different sizes.
* ​OneSignal - Free background push notifications using OneSignal.

### Service Worker

在 MDN 上的说明：

> Service workers 本质上充当Web应用程序与浏览器之间的代理服务器，也可以在网络可用时作为浏览器和网络间的代理。它们旨在（除其他之外）使得能够创建有效的离线体验，拦截网络请求并基于网络是否可用以及更新的资源是否驻留在服务器上来采取适当的动作。他们还允许访问推送通知和后台同步API。

其实不用太纠结，简单起见我们就把它当成更高级更先进的 AppCache 就好了。

### 学习资料

* [Google Tutorials](https://codelabs.developers.google.com/codelabs/your-first-pwapp/#0)
* [百度 Lavas（基于 vue 的 PWA 方案）](https://lavas.baidu.com/)
* [google-app demo](https://github.com/GoogleChromeLabs/squoosh/)



