# ACL(Access Control List)

```shell
#登录zkCli.sh
#添加用户
addauth digest username:password:cdrwa
#在zookeeper中密码以密文方式存储
setAcl /dubbo digest:username:密文密码:cdrwa

#以上是设置，接下来是验证
#重新登录
ls /dubbo
#没有权限
addauth digest username:password
ls /dubbo
#成功

#父子节点权限没有继承关系

```







# 设置鉴权

