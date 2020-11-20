### Web登录那些事儿

##### Cookie、Session

流程：

* 客户端用用户名和密码请求login接口，服务器端收到后校验数据，校验正确就会在服务器端存储一个sessionId和session的映射关系
* 服务器端返回response，并将sessionId以set-cookie的方式放在客户端。
* 客服端发起非登录请求时，会自动在头部带上cookie信息，服务器端获取cookie中的sessionId找到对应的session来确定请求者。

缺点：

1. cookie会有csrf攻击
2. http请求携带cookie，如果cookie过大，会增加http请求的带宽
3. 因为cookie不支持跨域，如果不是单台服务器，就需要在服务器间共享session数据，让每台服务器都能读取session。
4. session数量随着登录用户的增多而增多，存储量会增加很多，占用大量服务器内存。

##### SessionSigned Cookie

介于cookie存储在客服端，可以被用户修改，所以加上签名来判断数据是否被篡改。

流程：

* 服务器提供签名生成算法secret
* 根据方法生成签名(例如原本cookie内有个字段`key1=keyword`, `secret(key)=98Uilyu1`);
* 将生成的签名放回对应的Cookie项`key1=keyword|98Uilyu1`。内容和签名用"|"隔开。
* 服务端根据接收到的内容和签名，校验内容是否被篡改。

##### JWT + Token

JWT(JSON Web Token), 简单来说JWT就是把用户信息转成base64加上签名返回给前端，由前端存储，每次请求带上，后端通过签名判断令牌是否新鲜并有效，如果正确，直接使用用户信息。

JWT由3部分组成：头部(Header)、负载(Payload)和签名(Signature)

* 头部(Header): 类型和签名算法，经过base64后的编码
* 负载(Payload): 存储有效信息，经过base64后的编码
* 签名(Signature): 由指定的算法，将转义后的头部和负载，加上密钥一同加密得到的。

最后的Token = 最后将这三部分用.号连接

JWT令牌一般存储在sessionStorage、localStorage里，通过HTTP的`Authorization: Bearer <token>`传输。

优点：

1. 服务器不需要保存令牌或当前session的记录，不管跨域还是集群，都可以获取用户信息

注意点：

1. Token 在服务器没有存储, 不能随时废除这个签名, 只能通过设置过期时间来让Token失效, 在到期之前都有效，不过服务器可以加一些逻辑解决这个问题。
2. JWT本身并没有加密性，只是用来解决会话问题的，加密的机制需要后台处理。所以负载(Payload)部分不要放敏感信息，很容易被解码出来。
3. refresh token, 服务器不需要刷新token的过期时间，一旦token过期，反馈给前端，前端用refresh token申请一个新的token继续使用。这样服务器只需要在客户端请求更新token的时候对refresh token的有效性进行一次检查，大大减少了更新有效期的操作，避免了频繁的读写。

##### Oauth

通过一个授权层隔离了客户端与用户信息，并在授权层基础上使用了一把安全的钥匙来代替用户完成授权。

流程：

* 用户打开客户端以后，客户端要求用户给与授权
* 用户同意并返回code
* 使用code换取token
* 返回请求token
* 携带token请求资源
* 返回请求资源


##### SSO

实现单点登录，服务器只需要维护一张userID和token之间的映射关系表。每次登录成功都刷新token的值。在处理业务逻辑之前，使用解密拿到的userId去映射表中找到token，和请求中的token对比来校验是否合法。

##### 扫码登录

todo


参考资料：
[Cookie防篡改机制](https://juejin.cn/post/6844903608618598407)
[常见登录认证 DEMO](https://juejin.cn/post/6844903895710302221)
[简单了解JWT](https://juejin.cn/post/6844904170072309768)
[理解OAuth 2.0](http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html)