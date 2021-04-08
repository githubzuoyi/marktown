# Dubbo

* dubbo的用途

* dubbo的基本使用
  * 相关配置



## 基本使用及文档参考



#### 配置

* 配置
  * 原则
    * 除了外围驱动方式上的差异（XML,ANNOTATION,API），Dubbo的配置读取总体上遵循了以下几个原则：
      * Dubbo 支持了多层级的配置，并按预定优先级自动实现配置间的覆盖，最终所有配置汇总到数据总线URL后驱动后续的服务暴露、引用等流程。
      * ApplicationConfig、ServiceConfig、ReferenceConfig 可以被理解成配置来源的一种，是直接面向用户编程的配置采集方式。
      * 配置格式以 Properties 为主，在配置内容上遵循约定的 `path-based` 的命名[规范](https://dubbo.apache.org/zh/docs/v2.7/user/configuration/configuration-load-process/#配置格式)
  * 配置来源（默认4种，优先级 从 高 到 低）
    * JVM System Properties，-D 参数
    * Externalized Configuration，外部化配置
    * ServiceConfig、ReferenceConfig 等编程接口采集的配置
    * 本地配置文件 dubbo.properties



* 外部化配置
  * 外部化配置目的

    * 外部化配置目的之一是实现配置的集中式管理，这部分业界已经有很多成熟的专业配置系统如 Apollo, Nacos 等，Dubbo 所做的主要是保证能配合这些系统正常工作。

  * 概览

    * 外部化配置和其他本地配置在内容和格式上并无区别，可以简单理解为 `dubbo.properties` 的外部化存储，配置中心更适合将一些公共配置如注册中心、元数据中心配置等抽取以便做集中管理。

  * 优先级

    * 外部化配置默认较本地配置有更高的优先级，因此这里配置的内容会覆盖本地配置值，关于 [各配置形式间的覆盖关系](https://dubbo.apache.org/zh/docs/v2.7/user/configuration/configuration-load-process) 有单独一章说明，你也可通过以下选项调整配置中心的优先级：

  * 作用域

    * 外部化配置有全局和应用两个级别，全局配置是所有应用共享的，应用级配置是由每个应用自己维护且只对自身可见的。当前已支持的扩展实现有Zookeeper、Apollo。

  * 引入配置中心

    * ```xml
      <dubbo:config-center address="zookeeper://127.0.0.1:2181"/>
      ```

  * dubbo对配置中心支持的本质

    * 所谓 Dubbo 对配置中心的支持，本质上就是把 `.properties` 从远程拉取到本地，然后和本地的配置做一次融合。理论上只要 Dubbo 框架能拿到需要的配置就可以正常的启动，它并不关心这些配置是自己加载到的还是应用直接塞给它的，所以Dubbo还提供了以下API，让用户将自己组织好的配置塞给 Dubbo 框架（配置加载的过程是用户要完成的），这样 Dubbo 框架就不再直接和 Apollo 或 Zookeeper 做读取配置交互。

    * 代码

      ```java
      // 应用自行加载配置
      Map<String, String> dubboConfigurations = new HashMap<>();
      dubboConfigurations.put("dubbo.registry.address", "zookeeper://127.0.0.1:2181");
      dubboConfigurations.put("dubbo.registry.simplified", "true");
      
      //将组织好的配置塞给Dubbo框架
      ConfigCenterConfig configCenter = new ConfigCenterConfig();
      configCenter.setExternalConfig(dubboConfigurations);
      ```