Nacos 中服务存储和数据存储的在外层都是一个名为 namespace 的东西，用来做在外层隔离。

* namespace：基于环境变量做隔离，例如有生产环境，开发环境，测试环境等等。
* group：分组，可以将一些业务相关度比较高的放在一个组里面。

## Namespace

新增命名空间

![[Pasted image 20220821145622.png]]

修改配置文件对应的命名空间，需要再对应的项目配置文件中修改

```yaml
spring:  
  cloud:  
    nacos:  
      server-addr: localhost:8848  
      discovery:  
        cluster-name: GZ  
        namespace: 62c75d23-5839-45db-bec9-8747fdcef332 # 命名空间ID
```

此时 public 和 dev 环境已被隔离，无法互相访问

![[Pasted image 20220821145950.png]]

#Nacos 