## spring必知必会 -- IOC

### API

* BeanFactory
* FactoryBean
* ApplicationContext
  * ApplicationEventPublisher
    * ApplicationListener 实现接口，监听事件发布
  * MessageResource
  * ResourcePatternResolver
  * LifeCycle
* WebApplicationContext



### 注意事项

* spring 容器灵活性高，可扩展性强的关键：
  * Note that the core `BeanFactory` API level and its `DefaultListableBeanFactory` implementation do not make assumptions about the configuration format or any component annotations to be used. All of these flavors come in through extensions (such as `XmlBeanDefinitionReader` and `AutowiredAnnotationBeanPostProcessor`) and operate on shared `BeanDefinition` objects as a core metadata representation. This is the essence of what makes Spring’s container so flexible and extensible.
* Bean
  * BeanFactory
  * FactoryBean
    * 通过工厂方法，来创建定制化的bean
    * 当调用getBean时，返回的对象不是FactoryBean本身，而是getObject方法返回的对象，如果需要工厂本身，则需要在前面加上&
    * 可以理解为Ioc容器创建bean的扩展，类似于 JAVA SE 的 ObectFactory
  * 实例化
    * BeanFactory
      * 第一次access时
    * ApplicationContext
      * 应用初始化时
  * 生命周期
    * BeanFactory
    * ApplicationContext
    * 调用链
* 上下文
  * BeanFactory 与 ApplicationContext的最大区别
    * 前者需要编程增加后置处理器，后者会通过反射读取配置中的后置处理器PostProcessor，并加载到应用上下文中
  * WEB
    * 通过ServletContext可以获得Spring应用上下文
      * WebApplicationContextUtils
    * spring应用上下文获取servletContext
      * getServletContext()
  * 后置处理器实现AOP

* Javabean
* 设计模式
  * 事件发布监听的设计模式
    * ApplicationEventPublisher  && ApplicationListener 





### 问题

* 梳理Servlet，WebApplicationContext的调用链，两个上下文是如何达到互访的
* spring IOC 实现原理
  * 依赖查找，注入
    * 反射
  * 属性编辑器
* spring生存周期
  * 实现
  * 设计思想
* 多个后置处理器 PostProcessor 调用顺序的实现
  * 设计模式
* 后置处理器实现AOP





# IOC 之 Bean 配置



## 问题汇总

* bean生命周期及管理（已经在IOC章讲述过了：beanFactory/applicationContext）
* bean的范围（及web下）
* Javabean 和 springbean的区别和联系
* bean的注入方式
* bean属性编辑器 && 类型转换（？）



## API



## 注意点

* bean配置信息，bean实现类，spring容器，应用程序关系表

  ![image-20210408083645422](C:\Users\左飞\AppData\Roaming\Typora\typora-user-images\image-20210408083645422.png)





## 扩展

* XML schema

  ![image-20210408084430906](C:\Users\左飞\AppData\Roaming\Typora\typora-user-images\image-20210408084430906.png)



## 问题

* spring bean实现了内部表示和外部定义的解耦，是怎么做到的？运用了什么设计模式
* 命名空间的作用