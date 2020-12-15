[toc]

# Ping实现

目的是使用c语言实现ping功能

ICMP(Internet Control Messages Protocol)英特网信报控制协议，是TCP/IP的一个子协议，是面向无连接的协议

ping命令实现原理：利用网络上机器的IP地址的唯一性，给目标地址发送一个苏举报，再要求对方返回一个同样大小的数据包



Ping命令只使用众多ICMP报文中的两种

"请求回送'(ICMP_ECHO)和"请求回应'(ICMP_ECHOREPLY)

两种的报头格式如下

![img](https://img-blog.csdn.net/20160603111250335)

