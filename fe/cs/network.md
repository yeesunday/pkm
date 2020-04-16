## 缓存策略

良好的缓存策略可以降低资源的重复加载提高网页的整体加载速度。通常浏览器缓存策略分为两种：

强缓存：Expires、Cache-Control

协商缓存：Last-Modified，If-Modified-Since 或 ETag、If-None-Match

优先级：Cache-Control > Expires > ETag、If-None-Match > Last-Modified，If-Modified-Since

原理：
1. 浏览器在加载资源时，根据请求头的expires和cache-control判断是否命中强缓存，是则直接从缓存读取资源，不会发请求到服务器。（200 from cache）
2. 如果没有命中强缓存，浏览器一定会发送一个请求到服务器，通过last-modified和etag验证资源是否命中协商缓存，如果命中，服务器会将这个请求返回，但是不会返回这个资源的数据，依然是从缓存中读取资源。（304）
3. 如果前面两者都没有命中，直接从服务器加载资源（200）

[浏览器缓存机制：强缓存、协商缓存](https://github.com/amandakelake/blog/issues/41)

## 状态码

301、302、307、308 的区别

|     | Permanent  | Temporary  |
|  ----  | ----  | ----  |
| Allows changing the request method from POST to GET. | 301 | 302 |
| Does not allow changing the request method from POST to GET.  | 307 | 308 |

[详解重定向（HTTP状态码301/302/303/307/408）](https://www.cnblogs.com/wuguanglin/p/redirect.html)