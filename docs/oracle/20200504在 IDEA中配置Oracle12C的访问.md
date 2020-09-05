# 在 IDEA中配置Oracle12C的访问



## 1、安装

- 点击maven栏目

![image-20200504165117937](D:\myBlogs\docs\oracle\image-20200504165117937.png)

输入命令：

```cmd
mvn install:install-file -Dfile=C:\Users\coder\Downloads\instantclient_12_2\ojdbc8.jar  -DgroupId=com.oracle -DartifactId=ojdbc8 -Dversion=12.2.0.1 -Dpackaging=jar
```

会显示安装成功

![image-20200504165319605](D:\myBlogs\docs\oracle\image-20200504165319605.png)



## pom.xml中引入

```xml
<dependency>
    <groupId>com.oracle</groupId>
    <artifactId>ojdbc8</artifactId>
    <version>12.2.0.1</version>
</dependency>
```



## 将MySql数据库作为开发环境

> 创建application-dev.yml

```xml
server:
  port: 9090
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/shop?serverTimezone=UTC&useUnicode=true&characterEncoding=UTF-8&useSSL=false
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
```



## 将Oracle数据库作为生成环境

> 创建application-prod.yml

```xml
server:
  port: 80
spring:
  datasource:
    url: jdbc:oracle:thin:@//192.168.31.51:1521/itpuxpdb
    username: fgedu
    password: fgedu
    driver-class-name: oracle.jdbc.OracleDriver
```

## 通用的配置还是留在著配置文件中

> application.yml中的内容

```xml
spring:
  thymeleaf:
    prefix: classpath:/templates/
    suffix: .html
    mode: HTML
    encoding: UTF-8
  profiles:
    active: prod
```

## 意外

> 其中使用了Oracle 的保留字段作为表名，user，出现了小问题，需要修改部门SQL语句，表名需要引号，并用\进行转义

```java
return jdbcTemplate.query("select * from \"user\"", new BeanPropertyRowMapper<>(User.class));
```

