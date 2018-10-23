## 微信开发注意事项

微信浏览器使用的是『自研』的 XT5 内核，所以有很多兼容性的问题需要特别留意

* 页面缓存和请求缓存。回退上一页时，微信不但会缓存住上页内容，get 请求也会缓存住，post 没有这个问题。解决页面缓存，可以：

```
window.onpageshow = function(event){
   if (event.persisted) {
       window.location.reload();
   }
};
```
解决请求缓存，可以加一个随机数作为请求参数。
