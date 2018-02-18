# 搭建redis集群(error) CLUSTERDOWN The cluster is down

标签（空格分隔）： redis

---

今天想搭建一个redis集群，搭建好一个简单的集群环境，准备简单测试一下
结果报错如下：
[root@centOS redis-cluster]# redis01/redis-cli -p 7004 -c
127.0.0.1:7004> set a 123
<font color="red">(error) CLUSTERDOWN The cluster is down</font>
经过一番排查，最终发现问题所在，当集群建立完毕linx问你是否确定的时我习惯性的打了一个'y'，但是他让我们输入的是'yes',以后要注意相关问题，如果有博友在搭建redis集群的时候遇到了<font color="red">(error) CLUSTERDOWN The cluster is down</font>问题，请检查是否和本人犯了同样的错误

Adding replica 192.168.25.128:7004 to 192.168.25.128:7001
Adding replica 192.168.25.128:7005 to 192.168.25.128:7002
Adding replica 192.168.25.128:7006 to 192.168.25.128:7003
M: b73a495f1438644a61f81d567aa201765ace30a9 192.168.25.128:7001
   slots:0-5460 (5461 slots) master
M: 8af49dcfaf62e66a70fe9665aca38bbb062f9ab0 192.168.25.128:7002
   slots:5461-10922 (5462 slots) master
M: e4714490f8f67f1437b968f8db5a6b81882443e2 192.168.25.128:7003
   slots:10923-16383 (5461 slots) master
S: 55bf6dd37078f9b550ffc1fb283facc797660f43 192.168.25.128:7004
   replicates b73a495f1438644a61f81d567aa201765ace30a9
S: 0d9421b739793b7f7bc22ea51e66dc25a02498d9 192.168.25.128:7005
   replicates 8af49dcfaf62e66a70fe9665aca38bbb062f9ab0
S: 9064a8a1592fe4db9196d9a0556e74b8f2b6c63a 192.168.25.128:7006
   replicates e4714490f8f67f1437b968f8db5a6b81882443e2
**Can I set the above configuration? (type <font color="red">'yes'</font> to accept): <font color="red">y</font>**
Aborting...

**最后本人通过kill -s 9 xxxx 来结束几个redis进程，然后重新启各个redis服务再搭建集群的方法解决了这个问题**

<font color="green">[root@centOS redis-cluster]# redis01/redis-cli -p 7004 -c
127.0.0.1:7004> set a 123
-> Redirected to slot [15495] located at 192.168.25.128:7003
OK</font>
记录下来给各位博友参考







