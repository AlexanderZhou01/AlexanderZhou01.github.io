# ActiveMq部署完毕访问报HTTP ERROR：503错误

标签（空格分隔）： ActiveMq

---

在linux上安装Activemq，启动正常，检查状态正常，但是访问的时候报HTTP ERROR：503错误，Proble accessing /.Reason: Service Unavailable Powered by Jetty://
老规矩复制错误代码看别人有没有类似的错误提示，但是很遗憾StackOverflow上对相关问题的回答和我的问题无关，
查了一下503错误相关问题
503 Service Unavailable 是一种HTTP协议的服务器端错误状态代码，它表示服务器尚未处于可以接受请求的状态。
通常造成这种情况的原因是由于服务器停机维护或者已超载。注意在发送该响应的时候，应该同时发送一个对用户友好的页面来解释问题发生的原因。该种响应应该用于临时状况下，与之同时，在可行的情况下，应该在 Retry-After 首部字段中包含服务恢复的预期时间。
缓存相关的首部在与该响应一同发送时应该小心使用，因为 503 状态码通常应用于临时状况下，而此类响应一般不应该进行缓存。

##我的解决办法
./activemq stop 停掉服务
./activemq console 查看日志
日志报错如下
<font color="red">java.net.UnknowHostException: zhh: zhh: unknown error</font>
因为我的主机名改为了zhh,hosts中写的却还是localhost 
所以<font color="red"> 需要修改hosts,在后面加上主机名zhh</font>
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4 <font color="red">zhh</font>
::1         localhost localhost.localdomain localhost6 localhost6.localdo

重新启动activemq,问题完美解决，早点查看日志就可以很快解决问题了，不能太依赖于搜索引擎了，如果有博友被这个问题折磨，希望能够帮到你







