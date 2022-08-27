Feign是声明式的 Web Service客户端，它让微服务之间的调用变得更简单了，类似 Controller 调用 Service。Spring Cloud 集成了 Ribbon 和 Eureka ，可在使用 Feign 时提供负载均衡的 HTTP 客户端。

## 使用方法

添加依赖

```xml
<dependency>  
    <groupId>org.springframework.cloud</groupId>  
    <artifactId>spring-cloud-starter-openfeign</artifactId>  
</dependency>
```

编写接口

```java
@FeignClient("userservice")  
public interface UserClient {  
  
    @GetMapping("/user/{id}")  
    User findById(@PathVariable("id") Long id);  
  
}
```

调用接口

```java
@Autowired  
private UserClient userClient;  
  
public Order queryOrderById(Long orderId) {  
    // 1.查询订单  
    Order order = orderMapper.findById(orderId);  
    User user = userClient.findById(order.getUserId());  
    order.setUser(user);  
    // 4.返回  
    return order;  
}
```


## 自定义配置

常用自定义配置

| 类型                  | 作用       | 说明                                      |
|:--------------------|:---------|:----------------------------------------|
|Logger.Level  | 修改日志级别   | 包含四种不同的级别：NONE / BASIC / HEADERS / FULL |
| Decoder | 响应结果的解析器 | http 远程调用的结果做解析，例如解析 Json 字符串为 Java 对象  |
| Encoder | 请求参数编码   | 将请求参数编码，便于通过 Http 请求发送                  |
| Contract      | 支持的注解格式  | 默认是 Spring MVC 的注解                      |
| Retryer       | 失败重试机制   | 请求失败的重试机制，默认是没有，不过会使用 Ribbon 的重试        |  

### 配置文件

全局日志配置

```yaml
feign:
  client:
    config:
      default:
        loggerLevel: FULL
```

局部日志配置（配置文件）

```yaml
feign:
  client:
    config:
      userservice:
        loggerLevel: FULL
```

### 配置类

配置类

```java
public class DefaultFeignConfiguration {  
  
    @Bean  
    public Logger.Level level () {  
        return Logger.Level.BASIC;  
    }  
  
}
```

全局日志配置

```java
@EnableFeignClients(defaultConfiguration = DefaultFeignConfiguration.class)
```


局部日志配置

```java
@FeignClient(value = "userservice", configuration = DefaultFeignConfiguration.class)
```

## 性能优化

Feign 性能优化主要包括两点：

1. 使用连接池代替默认的 URLConnection
2. 日志级别使用 BASIC 或 NONE

Feign 底层的客户端实现：

1. URL Connection：默认实现（JDK），不支持连接池
2. Apache HttpClient：支持连接池（推荐）
3. OKHttp：支持连接池（推荐）

### Apache HttpClient

引入依赖

```xml
<dependency>  
    <groupId>io.github.openfeign</groupId>  
    <artifactId>feign-httpclient</artifactId>  
</dependency>
```

修改配置

>max-* ，需根据真实情况调整

```yaml
feign:  
  httpclient:  
    enabled: true  
    max-connections: 200 # 最大连接数  
    max-connections-per-route: 50 # 每个路径的最大连接数
  client:  
    config:  
      default:  
        logger-level: BASIC
```

## 最佳实践

### 继承

给消费者的 FeignClient 和提供者的 Controller 定义统一的接口作为标准。

![[20220827164314.png]]

此方法会造成以下两种缺点，但是可以约束消费者和提供者，看情况使用

缺点：

* 服务紧耦合
* 父类方法参数中的映射不会被继承，例如：`@PathVariable` 注解

### 抽取

将 FeignClient 抽取为独立模块，并且把接口有关的 POJO 、默认的 Feign 配置都放到这个模块中，提供给所有消费者使用。

![[20220827164416.png]]
此方法耦合度降低。不过会造成多余的依赖类，例如 order-service 只需要 UserClient ，但是 feign-api 中，也提供了 PayClient ，这对于 orderservice 是多余的。