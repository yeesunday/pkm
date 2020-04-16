## window.performance

在开发环境下，其实我们自己打开 Chrome 的开发者工具，切换到网络面板，就能很详细的看到网页性能相关的数据。但当我们需要统计分析用户打开我们网页时的性能如何时，我们将 performance 原始信息或通过简单计算后的信息 (如上面写到的 getPerformanceTiming()  和 getEntryTiming()) 上传到服务器，配合其他信息（如 HTTP 请求头信息），就可以监控到用户端的表现数据。

[初探 performance – 监控网页与程序性能](http://www.alloyteam.com/2015/09/explore-performance/)