## 角色

* 服务提供者：启动时，向 Nacos 注册服务信息
* 服务消费者：定时（间隔30s）拉取服务（pull），将拉取的信息缓存在服务列表中。同时 Nacos 发现服务信息变更，会主动推送变更消息 （push）
* 注册中心：Nacox

![[Pasted image 20220821153345.png]]

## 实例

Nacos 会将服务提供者划分为 `临时实例` 和 `非临时实例` ，Nacos 对这两种实例的健康监测是不一样的。默认情况下：所有的实例都是临时实例。推荐临时实例，非临时实例对服务器压力大。

* 临时实例：采用心跳监测。如果服务不存在，从列表中删除。
* 非临时实例：Nacos 发起请求检测。如果服务不存在，并不会从列表中删除，而是标记不健康，等待恢复健康。

查看是否为临时实例
![[Pasted image 20220821150756.png]]

配置非临时实例，通过更改项目配置

```yaml
spring:  
  cloud:  
    nacos:  
      server-addr: localhost:8848  
      discovery:  
        cluster-name: GZ  
        namespace: 62c75d23-5839-45db-bec9-8747fdcef332 # 命名空间ID
        ephemeral: false # 非临时实例
```

#Nacos 