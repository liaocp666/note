## SpringBoot 版本命名规则

SpringBoot 通常采用数字来命名：主版本号 + 次版本号 + 修正版本号。


<!--more-->

### 数字版本解释

```xml
<!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot</artifactId>
    <version>2.6.0</version>
</dependency>
```
* 数字2：表示的主版本号，表示是我们的SpringBoot第二代产品，当功能模块有较大更新或者整体架构发生变化时，主版本号会更新。
* 数字6：表示的是次版本号，增加了一些新的功能但是主体的架构是没有变化的，是兼容的，只是局部的一些变动。
* 数字0：表示的一般是bug的修改或者是小的变动。

### 字母解释

在 Spring 网站页面 https://spring.io/projects/spring-boot#learn ，通常会带有一个字母小尾巴，不同的尾巴也有不同的含义：

![[Pasted image 20220817220003.png]]

* snapshot： 快照
* alpha ： 内测
* beta ： 公测
* release ： 稳定版本
* GA： 最稳定版本
* Final ： 正式版
* Pro(professional) ： 专业版
* Plus： 加强版
* Retail ： 零售版
* DEMO ： 演示版
* Build ： 内部标号
* Delux： 豪华版 （deluxe：豪华的，华丽的）
* Corporation或Enterpraise 企业版
* M1 M2 M3 ： M是milestone的简写 里程碑的意思
* RC 版本RC:(Release Candidate)，几乎就不会加入新的功能了，而主要着重于除错
* SR ： 修正版
* Trial ： 试用版
* Shareware ： 共享版
* Full ： 完全版

**名词解释**

build-snapshot： 开发版本，也叫快照版本。当前版本处于开发中，开发完成之后，自己进行测试，另外让团队其它人也进行测试使用下;

M1…M2（Milestone）： 里程碑版本，在版发布之前 会出几个里程碑的版本。使用snapshot版本开发了一个时间，觉得最近写代码杠杠的，那么就整几个里程碑版本记录下吧，记录我们这个重大的时刻，是你我未来的回忆。

RC1…RC2（Release Candidates）： 发布候选。内部开发到一定阶段了，各个模块集成后，经过细心的测试整个开发团队觉得软件已经稳定没有问题了，可以对外发行了。

release： 正式版本。发布候选差不多之后，那么说明整个框架到了一定的阶段了，可投入市场大面积使用了，那么发布出去，让广大用户来吃吃香吧。

SR1…SR2（Service Release）： 修正版。这是啥意思呐，这不release版本发布之后，让广大群体使用了嘛，再牛逼的架构师，也无法写出零bug的代码，那么这时候，就优先对于release版本的问题进行修复，这时候每次迭代的版本就是SR1,SR2,SR3。

**字母顺序**

snapshot –>M1…MX –> RC1…RCX –> release –> SR1…SRX

对应的文字理解：

开发版本(BS) --(开发到一个小阶段，就要标记下)–> 里程碑版本(MX) --(版本到了一个相对稳定的阶段，可以对外发行了，但是可能还存在修复的问题，此时只做修复，不做新功能的增加)–> 发布候选(RC1) --(BUG修复完成，发布)–>正式版本(release) --(外界反馈存在一些问题，进行内部在修复)–> 修正版本(SRX)

## SpringCloud 版本命名规则

从 Spring Cloud 2020.0.0-M1 开始，Spring Cloud 使用了全新的 "日历化" 版本命名方式来控制发布到中央仓库的版本。

* YYYY：表示 4 位年份；
* MINOR：代表一个递增的数字，每年以 0 开始递增；
* MICRO：代表版本号后缀，就和之前使用的 .0 类似于 .RELEASE 一样，.2 类似于 .SR2。

## SpringCloud 与 SpringBoot 版本对应

SpringCloud与SpringBoot版本，以 Spring Cloud 的版本为主，然后去选择对应的 Spring Boot 版本。

打开Spring Cloud官方网站：https://docs.spring.io/spring-cloud/docs/current/reference/html/ ，在此页面的第一段话下面，就可以看到目前SpringCloud发行版，并与之对应的SringBoot版本。

![[Pasted image 20220817220034.png]]

如果需要更加详细的版本对应，打开此网站 https://start.spring.io/actuator/info ，格式化对应JSON就可以看到了

![[Pasted image 20220817220050.png]]
![2662390602](https://www.kokoo.top/upload/2022/08/2662390602.png)

>参考文章：
>1. https://blog.csdn.net/Thinkingcao/article/details/108362819
>2. https://spring.io/blog/2020/04/17/spring-cloud-2020-0-0-m1-released