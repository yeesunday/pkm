## XSS 和 CSRF

XSS，即 Cross Site Script，中译是跨站脚本攻击，是指攻击者在网站上注入恶意的客户端代码，通过恶意脚本对客户端网页进行篡改，从而在用户浏览网页时，对用户浏览器进行控制或者获取用户隐私数据的一种攻击方式。防范：

1. HttpOnly 防止劫取 Cookie
2. 输入检查，对于用户的任何输入要进行检查、过滤和转义。建立可信任的字符和 HTML 标签白名单，对于不在白名单之列的字符或者标签进行过滤或编码。
3. 输出检查，在变量输出到 HTML 页面时，可以使用编码或转义的方式来防御 XSS 攻击。

CSRF，即 Cross Site Request Forgery，中译是跨站请求伪造，是一种劫持受信任用户向服务器发送非预期请求的攻击方式。防范：

1. 使用验证码强迫用户与应用交互，进行意愿验证
2. Referer Check
3. Set-Cookie: SameSite；

SameSite 值：Strict、Lax、None

XSS 篡改网站，CSRF 冒充用户。XSS 的 Cross Site主要是指在本网站运行了来自其他网站的脚本，而 CSRF 的Cross Site则相反，指在其他网站对本网站造成了影响。跟 XSS 相比，XSS 利用的是用户对指定网站的信任，CSRF 利用的是网站对用户网页浏览器的信任。

[Cookie 的 SameSite 属性](https://www.ruanyifeng.com/blog/2019/09/cookie-samesite.html)

