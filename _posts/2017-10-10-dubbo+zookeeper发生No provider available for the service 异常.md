# dubbo+zookeeper发生No provider available for the service异常

标签（空格分隔）： dubbo

---

异常代码如下：
**java.lang.IllegalStateException**: Failed to check the status of the service cn.e3mall.service.ItemCatService. **No provider available for the service** cn.e3mall.service.ItemCatService from the url zookeeper://192.168.25.128:2181/com.alibaba.dubbo.registry.RegistryService?application=e3-manager-web&dubbo=2.5.3&interface=cn.e3mall.service.ItemCatService&methods=getItemCatlist&pid=6240&revision=0.0.1-SNAPSHOT&side=consumer&timestamp=1518769931967 to the consumer 169.254.200.97 use dubbo version 2.5.3
	com.alibaba.dubbo.config.ReferenceConfig.createProxy(ReferenceConfig.java:420)
	com.alibaba.dubbo.config.ReferenceConfig.init(ReferenceConfig.java:300)
	com.alibaba.dubbo.config.ReferenceConfig.get(ReferenceConfig.java:138)
	com.alibaba.dubbo.config.spring.ReferenceBean.getObject(ReferenceBean.java:65)
	org.springframework.beans.factory.support.FactoryBeanRegistrySupport.doGetObjectFromFactoryBean(FactoryBeanRegistrySupport.java:168)
	org.springframework.beans.factory.support.FactoryBeanRegistrySupport.getObjectFromFactoryBean(FactoryBeanRegistrySupport.java:103)
	org.springframework.beans.factory.support.AbstractBeanFactory.getObjectForBeanInstance(AbstractBeanFactory.java:1585)
	org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:254)
	org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:197)
	org.springframework.beans.factory.support.DefaultListableBeanFactory.findAutowireCandidates(DefaultListableBeanFactory.java:1192)
	org.springframework.beans.factory.support.DefaultListableBeanFactory.doResolveDependency(DefaultListableBeanFactory.java:1116)
	
	
出现这个问题首先复制错误代码Google了一下，Google对与dubbo的问题并没有给出多少有价值的提示，转而寻求百度，百度这个不争气的儿子竟然给出了一大堆相关的答案，不知道是不是我当时的搜索关键词太长了还是因为百度这个不争气的儿子终于开始浪子回头了，（个人一直认为百度的技术还是不差的），说着说着就走题了，在网上查到可能的原因如下

<font color="red">1.配置文件中dubbo相关的配置书写错误</font>
        1）最简单的拼写错误
        2）如果生产者设定了服务的版本version，消费者一定要提供相应的版本号（好多人是这个问题导致的）
        
<font color="red">2.zookeeper和dubbo的2181端口以及20880端口开放问题，端口未开放导致出现了无法提供服务的问题</font>
检查服务器的端口开放情况，查看dubbo和zookeeper相关的端口配置

<font color="red">3.本人出现错误的原因：</font>
我在web-manager模块的web层中要用到web-content模块中的服务，本来直接在web-manager的消费者中直接引用就好，但是一不小心在web-manager的生产者dubbo配置文件中配置了web-content的服务内容，也就是这里生产者配置了一个服务，但是这个模块无法获取，可以错误信息却显示的是这里有另一个本地服务无法获取，导致自己无法联想到是这里web-manager中写了一个其他的服务，一直在排查拼写错误和服务器端口，浪费了许多时间，写一篇博客纪念一下愚蠢的自己，编程是一个修行的过程，静下心来，脚踏实地，一步步的向下一个层次进发。



