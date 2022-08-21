Eureka 是 Netflix 开发的服务发现框架，本身是一个基于 REST 的服务，主要用于定位运行在 AWS 域中的中间层服务，以达到负载均衡和中间层服务故障转移的目的。 Spring Cloud 将它集成在其子项目 spring-cloud-netflix 中，以实现 Spring Cloud 的服务发现功能。

## Eureka 角色

在 Eureka 架构中，微服务角色有两类：

**Eureka Server：服务端，注册中心**

* 记录服务信息
* 心跳监控

**Eureka Client：客户端**

* Provider：服务提供者
	* 注册自己的信息到 Eureka Server
	* 每隔 30 秒向 Eureka Server 发送心跳
* Consumer：服务消费者
	* 根据服务名称从 Eureka Server 拉取服务列表
	* 基于服务列表做负责均衡，选中一个微服务后发起远程调用

## 搭建 Eureka Server

1. 创建项目，引入下面依赖
```xml
<!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-netflix-eureka-server -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```
2. 启动类上增加 `@EnableEurekaServer` 注解
3. 在 `application.yml` 文件，添加相关配置
```yaml
server:  
  port: 10086  
  
spring:  
  application:  
    name: eurekaserver  
  
eureka:  
  instance:  
    hostname: localhost  
  client:  
    service-url:  
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
```

## 搭建 Eureka Client

1. 引入依赖
```xml
<!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-netflix-eureka-client -->
<dependency>  
    <groupId>org.springframework.cloud</groupId>  
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>  
</dependency>
```
2. 添加配置
```yaml
spring:
  application: user-servier
eureka:  
  instance:  
    hostname: localhost  
  client:  
    service-url:  
      defaultZone: http://${eureka.instance.hostname}:10086/eureka/
```