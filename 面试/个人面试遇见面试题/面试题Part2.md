spring了解多少 ？

首先，Spring是一个轻量级的JavaEE框架。在Spring的官方参考手册中可以知道，官方对他的定义是:Spring 是一个轻量级的，非侵入式的框架，提供一站式服务，开发者可以根据自己的需求选择不同的组件，所以被称为框架的框架。另外，Spring的一个重要理念就是约定优于配置。



spring cloud主要项目有哪些？（通过spring官方文档查询）

Spring Cloud Config、Spring Cloud Netflix、Spring Cloud Bus、Spring Cloud Cloudfoundry、Spring Cloud Open Service Broker、Spring Cloud Cluster、Spring Cloud Consul、Spring Cloud Security、Spring Cloud Sleuth、Spring Cloud Data Flow、Spring Cloud Stream、Spring Cloud Stream App Starters、Spring Cloud Task、Spring Cloud Task App Starters、Spring Cloud Zookeeper、Spring Cloud AWS、Spring Cloud Connectors、Spring Cloud Starters、Spring Cloud CLI、Spring Cloud Contract、Spring Cloud Gateway、Spring Cloud OpenFeign、Spring Cloud Pipelines、Spring Cloud Task、

值得一提的是 Spring Cloud Netflix项目，它整合了我们平时用的最多的那些组件，比如说：Eureka、Hystrix,Zuul、Archaius等等



myql的事务以及事务的隔离级别

ACID:分别代表原子性、一致性、隔离性和持久性

隔离级别：Read uncommitted、Read committed、Repeatable read 、Serializable

一般各大数据库的默认事务级别是Read Committed