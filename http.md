### http

#### 协议

- http和tcp connetior关系?
  - http 只有请求和响应他是通过tcp connection与服务器建立连接的
- 为什么要3次握手?
  - 为了防止服务端开启无用的链接,网络传输是有延时的,有可能在传输过程中丢失了内容,客户端就没有接收到可能设置了超时时间就关闭了,但不知道服务端是不知道的,服务端一直开着端口等着开销浪费

#### TCP链接(长链接/短链接)

- http请求是在tcp链接上发送的,请求-链接-返回.服务端和客户端商量要不要把这个链接关闭掉,一直开着会有消耗,如果还有请求,就可以还在这个tcp上,不需要经过三次握手
- 如果关闭了,下次还有请求,就重新创建链接,减少并发链接数;

#### 跨域
- 其实已经发出了,并得到响应,但是浏览器端会根据请求头的Access-Control-Allow-Origin识别允许的请求,假如未通过浏览器会阻止,并抛出异常

#### 缓存

- max-age=55000缓存时间
-  no-cache不能直接使用缓存,要去服务器验证
  - Last-Modified || Etag 来设置缓存(设置缓存)
  - If-Modified-Since: 'xxx' || If-None-Match:'xxx'要去服务器验证是否可以读取本缓存
  - 因为设置了客户端缓存了,前端假如内容变化发布,服务器无法得知,打包时有对应的hash值变化,所以请求的url变化所以会有最新代码
  - ![1594564426263](C:\Users\CH\AppData\Roaming\Typora\typora-user-images\1594564426263.png)
- no-store 忽略任何缓存信息,这是一个全新的请求

