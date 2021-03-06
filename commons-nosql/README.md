# Commons NOSQL Component
## 1. MongoDB

> The Spring Data MongoDB 2.x binaries require JDK level 8.0 and above and [Spring Framework](https://spring.io/docs) 5.1.5.RELEASE and above.
>
> In terms of document stores, you need at least version 2.6 of [MongoDB](https://www.mongodb.org/).

依赖包Maven坐标如下：

```xml
<properties>
    <!--<mongodb.version>2.9.3</mongodb.version>-->
    <mongodb.version>3.10.1</mongodb.version>
    <spring.data.version>2.1.5.RELEASE</spring.data.version>
</properties>
<!--mongodb驱动包：包括bson，mongo-java-drive和mongo-java-core-->
<dependency>
    <groupId>org.mongodb</groupId>
    <artifactId>mongodb-driver</artifactId>
    <version>${mongodb.version}</version>
</dependency>
<!--mongodb Spring核心包-->
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-mongodb</artifactId>
    <version>${spring.data.version}</version>
    <exclusions>
        <exclusion>
            <groupId>org.mongodb</groupId>
            <artifactId>mongo-java-driver</artifactId>
        </exclusion>
        <exclusion>
            <groupId>org.springframework.data</groupId>
            <artifactId>spring-data-commons</artifactId>
        </exclusion>
    </exclusions>
</dependency>
<!--mongodb Spring依赖包-->
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-commons</artifactId>
    <version>${spring.data.version}</version>
    <scope>compile</scope>
</dependency>
```
## 2. MemCache

## 3. Redis

### 3.1 Maven依赖

> Spring Data Redis 2.x binaries require JDK level 8.0 and above and Spring Framework 5.1.5.RELEASE and above.
> 
> In terms of key-value stores, Redis 2.6.x or higher is required. Spring Data Redis is currently tested against the latest 4.0 release.

Redis 依赖Maven坐标

```xml
<!--redis-->
<properties>
    <!--redis-->
    <jedis.version>2.10.0-m1</jedis.version>
    <spring.data.redis.version>2.1.5.RELEASE</spring.data.redis.version>
</properties>

<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>${jedis.version}</version>
</dependency>
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-redis</artifactId>
    <version>${spring.data.redis.version}</version>
    <exclusions>
        <exclusion>
            <groupId>org.springframework</groupId>
            <artifactId>spring-tx</artifactId>
        </exclusion>
        <exclusion>
            <groupId>org.springframework</groupId>
            <artifactId>spring-oxm</artifactId>
        </exclusion>
        <exclusion>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
        </exclusion>
        <exclusion>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context-support</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

### 3.2 Jedis旧版本问题

Jedis版本为2.2.1会出现如下问题，**Jedis对象正好有一个名字叫做shutdown的方法，虽然Jedis对象没有指定destoryMethod，但是被Spring 自动推断注册成为了DisposableBean！！！并且把shutdown()方法注册为destoryMethod，在程序运行结束的时候会调用shutdown()，发送SHUTDOWN关闭了Redis服务器！！！**