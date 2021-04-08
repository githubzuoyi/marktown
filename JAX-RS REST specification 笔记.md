## JAX-RS REST specification 笔记

### 关键API

* Application
  * 服务入口
* Providers
  * 辅助REST框架完成过滤或读写拦截
  * AOP
  * 绑定
    * 注册到Application
    * @provider
    * @Namebinding

### 关键点



### 扩展延伸

* 参考实现
  * http://jersey.java.net/
    * api
    * 操作手册
  * JBoss - RESTEasy : http://resteasy.jboss.org   +  /docs.html
* 了解glassfish生态
  * HK2 ~~ spring di
  * EclipseLink
  * Open MQ: https://mq.java.net
  * OpenJDK:http://openjdk.java.net
* 参考书籍
  * Java RESTful web 实战
* 规范
  * 依赖注入规范 JSR 330



### 问题

* 为什么说REST 是一种架构风格，它是什么样的一种架构风格？
  * REST服务：ORA - 面向资源的架构