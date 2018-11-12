### 解决目标

正如官网所说：

> 2016 年 10 月 25 日，zeit.co 背后的团队对外发布了 Next.js，一个 React 的服务端渲染应用框架。几小时后，与 Next.js 异曲同工，一个基于 Vue.js 的服务端渲染应用框架应运而生，我们称之为：Nuxt.js。

> Nuxt.js 是一个基于 Vue.js 的通用应用框架。
通过对客户端/服务端基础架构的抽象组织，Nuxt.js 主要关注的是应用的 UI渲染。
我们的目标是创建一个灵活的应用框架，你可以基于它初始化新项目的基础结构代码，或者在已有 Node.js 项目中使用 Nuxt.js。
Nuxt.js 预设了利用Vue.js开发服务端渲染的应用所需要的各种配置。

简而言之，Nuxt.js是帮助Vue.js轻松完成服务端渲染工作的框架。Nuxt.js预设了服务端渲染所需要的各种配置，如异步数据，中间件，路由。它好比是 Angular Universal 之于 Angular， Next.js 之于 React。

### 静态文件生成器

Nuxt.js的一个重要功能是，通过 generate 命令，生成静态站点。类似于流行的静态生成工具Jekyll。

### Nuxt.js 内部依赖

除了Vue.js 2.0之外，Nuxt.js集成了如下模块: Vue-Router, Vue-Meta 和 Vuex (仅在使用 Vuex 状态树配置项 时引入)。 这样的好处在于，不需要手工配置依赖，不需要同时在客户端和服务端配置相同的库。 Nuxt.js在包含如上依赖的情况下，总大小仍然保持在 28kb min+gzip (如果使用了 Vuex 特性的话为 31kb)。

另外，Nuxt.js 使用 Webpack 和 vue-loader 、 babel-loader 来处理代码的自动化构建工作（如打包、代码分层、压缩等等）。

### 工作原理

当你访问一个基于Nuxt.js构建的页面时，发生了的事情如下：

1. 当用户访问应用程序, 如果store中定义了 nuxtServerInit action，Nuxt.js将调用它更新store。

2. 接下来，将加载即将访问页面所依赖的任何中间件。Nuxt首先从nuxt.config.js这个文件中，加载全局依赖的中间件，之后检测每个相应页面对应的布局文件 ，最后，检测布局文件下子组件依赖的中间件。以上是中间件的加载顺序。

3. 如果要访问的路由是一个动态路由, 且有一个相应的 validate() 方法路由的validate 方法，讲进行路由校验。

4. 之后, Nuxt.js 调用 asyncData() 和 fetch() 方法，在渲染页面之前加载异步数据。asyncData() 方法用于异步获取数据，并将fetch回来的数据，在服务端渲染到页面。 用fetch() 方法取回的将数据在渲染页面之前填入store。

5. 最后一步, 将所有数据渲染到页面。

![](https://zh.nuxtjs.org/nuxt-schema.png)