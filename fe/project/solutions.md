## 大文件上传

大文件上传，要实现以下需求：
1. 文件切片
2. 文件还原（后端）
3. 断点续传
4. 上传进度和暂停上传

可以利用 `Blob` 对象的 `slice` 方法切片，对切片建立索引，可以实现上传和还原的管理。

[前端大文件上传](https://juejin.im/post/5cf765275188257c6b51775f)

## 直播

* HLS：跨平台、延迟高(10~20s)
* RTMP：浏览器需要借助 flash，延迟低（1~3s）

[h5直播技术探索](https://hellohy.github.io/post/vue-hls/)

[H5 直播起航](https://juejin.im/entry/6844903447657988104)