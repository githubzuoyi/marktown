## JMS 与 reactive stream

### 响应式流 reactive stream

#### 概念

> Reactive Stream (响应式流/反应流) 是JDK9引入的一套标准，是一套基于发布/订阅模式的数据处理规范。响应式流从2013年开始，作为提供非阻塞背压的异步流处理标准的倡议。 它旨在解决处理元素流的问题——如何将元素流从发布者传递到订阅者，而不需要发布者阻塞，或订阅者有无限制的缓冲区或丢弃。更确切地说，**Reactive流目的是“找到最小的一组接口，方法和协议，用来描述必要的操作和实体以实现这样的目标：以非阻塞背压方式实现数据的异步流”**。

* 官方wiki
  * https://github.com/reactive-streams/reactive-streams-jvm/blob/v1.0.3/README.md

* 原理图

![img](https://pic1.zhimg.com/80/v2-5331938a6745f7ee5eb8047a21f994c0_720w.jpg)



* 相应实现
  * 官方实现
    *  https://github.com/reactive-streams/reactive-streams-jvm/tree/master/examples/src/main/java/org/reactivestreams/example/unicast



### JMS



##### 关键 API

* ConnectionFactory
  * an administered object used by a client to create a  Connection
* Connection
  * an active connection to a JMS provider
* Destination
  *  an administered object that encapsulates the identity of a message destination
* Session
  *  a **single-threaded** context for sending and receiving messages
* MessageProducer
  *  an object created by a Session that is used for sending messages to a destination
* MessageConsumer
  * an object created by a Session that is used for receiving messages sent to a destination



##### JMS OBJECT RELATIONSHIP

![image-20210404100116154](C:\Users\左飞\AppData\Roaming\Typora\typora-user-images\image-20210404100116154.png)



#### 消息模型

* Goals
  * Provide a single, unified message API
  * Provide an API suitable for creating messages that match the format used by existing, non-JMS applications
  * Support the development of heterogeneous applications that span operating systems, machine architectures, and computer languages
  * Support messages containing Java objects
  * Support messages containing Extensible Markup Language pages (see http://www.w3.org/XML).
* Message header field
  * **JMSCorrelationID**
* how message header values are set
  * ![image-20210404105157955](C:\Users\左飞\AppData\Roaming\Typora\typora-user-images\image-20210404105157955.png)





#### 注意点

* 目标

* 注意点

  * 一个典型的JMS应用的创建过程

    * ```java
      A typical JMS client executes the following JMS setup procedure:
      • Use JNDI to find a ConnectionFactory object
      • Use JNDI to find one or more Destination objects
      • Use the ConnectionFactory to create a JMS Connection with message delivery inhibited
      • Use the Connection to create one or more JMS Sessions
      • Use a Session and the Destinations to create the MessageProducers and MessageConsumers needed
      • Tell the Connection to start delivery of messages
      ```

  * multithreading

    * 图解
      * ![image-20210404101311682](C:\Users\左飞\AppData\Roaming\Typora\typora-user-images\image-20210404101311682.png)
    * Session不支持并发的原因
      *  First, Sessions are the JMS entity that supports transactions. It is very difficult to implement transactions that are multithreaded.
      * **Second, Sessions support asynchronous message consumption**

  * messaging style

    * PTP
    * Pub/Sub
    * API
      * ![image-20210404095447206](C:\Users\左飞\AppData\Roaming\Typora\typora-user-images\image-20210404095447206.png)

  * administrator

    * ![image-20210404095018662](C:\Users\左飞\AppData\Roaming\Typora\typora-user-images\image-20210404095018662.png)

  * Request/Reply

    * 

  * 事务

    * JAVA JDBC
    * JTA 
      * A JMS provider can optionally support distributed transactions via JTA

* 相关规范
  * EJB 2.0
  * JTA
  * JTS





#### 问题汇总

* Session不支持并发的原因讨论
  * Sessions support asynchronous message consumption