# 学习TCP

## 三次握手

1. SYN：client 随机生成起始分组序列号 x ，并发送SYN分组，还有其他TCP表示和选项
2. SYN ACK：server 将 x+1 ，生成随机序列号 y
3. ACK：client 将 x + 1，y + 1，发送ACK分组，完成握手。此时可以发起请求，比如 Http Get 。

## 慢启动

完成了三次握手，client发送了http/get请求，server处理完请求开始发送响应数据，新TCP链接传输的最大值取rwnd和cwnd的最小值，也就是4个TCP段。client收到4个TCP段后分别发送ACK确认，也就是4个ACK确认。server收到4个ACK，每收到一个ACK，慢启动算法会让服务器cwnd递增一个TCP段，此时cwnd就增加到8个TCP段。这就是慢启动和指数增长。

rwnd
: 缩放窗口

cwnd
: 拥塞窗口

TCP段
: 一个TCP数据包。负载1460字节 + TCP头信息20字节 + IP头信息20字节 + 以太网头信息22字节 = 以太网数据包1522字节

4个TCP段
: 协议规定的服务器默认cwnd值，新版协议是10个。

## 参考
1. 阮一峰.[TCP 协议简介](http://www.ruanyifeng.com/blog/2017/06/tcp-protocol.html).[2017年6月8日]
1. Ilya Grigorik.Web性能权威指南.李松峰译.北京:人民邮电出版社，2014
