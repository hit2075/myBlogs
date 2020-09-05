# vhr  踩坑



- tomcat启动后的中文乱码

> 打开cd到tomcat/conf/目录下
>
> 修改logging.properties
>
> 找到
>
> java.util.logging.ConsoleHandler.encoding = utf-8这行
>
> 更改为
>
> java.util.logging.ConsoleHandler.encoding = GBK

- 启动时出现

```xml
No bean named 'cacheManager' available
```

> spring-servlet中我们引入了cache的同名库
>
> ```xml
> <mvc:annotation-driven/>
> ```
>
> 删掉原来的，重新引入xmlns:mvc="http://www.springframework.org/schema/mvc"，表空间
>
> 重新部署后恢复