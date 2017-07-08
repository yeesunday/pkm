## 学习资料
* express 
    * 中文文档 http://javascript.ruanyifeng.com/nodejs/express.html
    * 项目例子 https://github.com/nswbmw/N-blog
* koa https://github.com/17koa/koa-generator-examples

## Note

* 使用 [nvm](https://github.com/creationix/nvm) 管理 node 版本
* 当你需要去多个源(一般是小于 10 个)汇总数据的时候，用 eventproxy 方便；当你需要用到队列，需要控制并发数，或者你喜欢函数式编程思维时，使用 async。大部分场景是前者，所以我个人大部分时间是用 eventproxy 的。
*  nodemon https://github.com/remy/nodemon  watch 代码改动
*  正则表达式
    *  https://deerchao.net/tutorials/regex/regex.htm
* mongodb
* [cross-env](https://www.npmjs.com/package/cross-env) 兼容 windows 的环境变量设置
* supervisor 会监听当前目录下 node 和 js 后缀的文件，当这些文件发生改动时，supervisor 会自动重启程序。

