## 新增配置 

* DataID：需要唯一不重复，建议使用 `微服务名称 + 环境名 + 后缀名(yaml等)`

![[Pasted image 20220821162036.png]]

## 启动流程

1. 项目启动
2. 读取 `Nacos` 配置文件，通过 `bootstrap.yml` 文件
3. 读取本地配置文件 `application.yml`
4. 创建 Spring 容器
5. 加载 bean
6. ……

## 读取配置

1. 引入客户端依赖
```xml
<dependency>  
    <groupId>com.alibaba.cloud</groupId>  
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>  
</dependency>
```

2. 在项目的 resource 目录新增 bootstrap.yml 文件，此文件是引导文件，优先级高于 application.yml
```yaml
spring:  
  application:  
    name: userservice  
  profiles:  
    active: dev # 开发环境  
  cloud:  
    nacos:  
      server-addr: localhost:8848 # Nacos 地址  
      config:  
        file-extension: yaml # 文件后缀名
```

## 热更新

Nacos 中的配置文件变更后，微服务可以无需重启应用变更后的配置。

* 方式一：在 `@Value` 注入变量所在类上添加注解 `@RefreshScope`
* 方式二（推荐）：使用 `@ConfigurationProperties` 注解，配合配置类使用

## 多环境共享

微服务启动，会从 Nacos 读取多个配置文件

* [spring.application.name]-[spring.profiles.active].yaml，例如：userservice-dev.yaml
* [spring.application.name].yaml，例如：userservice.yaml

其中 `[spring.application.name].yaml` 文件是不变的，而且一定会被加载，因此多环境共享配置，可以写入这个文件。

![[Pasted image 20220821164556.png]]

## 优先级

从高到低排序：

1. [spring.application.name] - [spring.profiles.active].yaml
2. [spring.application.name].yaml
3. application.yml

#Nacos 