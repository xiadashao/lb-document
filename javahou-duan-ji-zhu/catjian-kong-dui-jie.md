# dubbo使用cat监控

## 1. 项目加入依赖的jar包

```
        <dependency>
            <groupId>com.lbonline</groupId>
            <artifactId>commom.util</artifactId>
            <version>1.0.0-RELEASE</version>
        </dependency>
```

## 2. 加入cat的AOP

**切点需要自定义！！！**

```
import com.lbonline.common.cat.aop.CatAop;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Pointcut;
import org.springframework.stereotype.Component;

@Component
@Aspect
public class CatConfig extends CatAop {

    @Override
    @Pointcut("execution(* com.lbonline.tms.service..*.*(..))")
    public void excudeService(){}

}
```

### 3.配置app和dubbo-filter

1.在resources资源文件META-INF下，注意是src/main/resources/META-INF/文件夹， 而不是webapps下的那个META-INF,添加app.properties文件，内容为：

```
app.name=tms-service
```

2.创建com.alibaba.dubbo.rpc.Filter文件，编辑文件加入以下内容：

```
catTransaction=com.lbonline.common.cat.filter.CatTransaction
```

###  4.application.yml配置

项目只有消费者只加消费者，有提供者只加提供者，都有就都加，如下例:

```
    consumer:
      filter: catTransaction
```

```
    provider:
      filter: catTransaction
```

### 5. 项目部署的服务器配置client.xml

在项目部署的服务器上创建/data/appdatas/cat/client.xml,此文件有OP控制,这里的Domain名字用来做开关，如果一台机器上部署了多个应用，可以指定把一个应用的监控关闭。注意这里的目录必须要有读写权限。**联系运维@夏康进行配置**

```
<?xml version="1.0" encoding="utf-8"?>
<config mode="client">
    <servers>
       <server ip="172.17.14.186" port="2280" http-port="8080" />
    </servers>
    <domain id="tms-service" enabled="true"/>
    <domain id="tms-web" enabled="true"/>
</config>
```

# web使用cat监控

## 1. 项目加入依赖的jar包

```
        <dependency>
            <groupId>com.lbonline</groupId>
            <artifactId>commom.util</artifactId>
            <version>1.0.0-RELEASE</version>
        </dependency>
```

## 2.引入cat过滤器

```
import com.dianping.cat.servlet.CatFilter;
import org.springframework.boot.web.servlet.FilterRegistrationBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;


@Configuration
public class CatFilterConfigure {

    @Bean
    public FilterRegistrationBean catFilter() {
        FilterRegistrationBean registration = new FilterRegistrationBean();
        CatFilter filter = new CatFilter();
        registration.setFilter(filter);
        registration.addUrlPatterns("/*");
        registration.setName("cat-filter");
        registration.setOrder(1);
        return registration;
    }
}
```

### 3.配置app和dubbo-filter

1.在resources资源文件META-INF下，注意是src/main/resources/META-INF/文件夹， 而不是webapps下的那个META-INF,添加app.properties文件，内容为：

```
app.name=tms-service
```

2.创建com.alibaba.dubbo.rpc.Filter文件，编辑文件加入以下内容：

```
catTransaction=com.lbonline.common.cat.filter.CatTransaction
```

###  4.application.yml配置

项目只有消费者只加消费者，有提供者只加提供者，都有就都加，如下例:

```
    consumer:
      filter: catTransaction
```

```
    provider:
      filter: catTransaction
```

### 5. 项目部署的服务器配置client.xml

在项目部署的服务器上创建/data/appdatas/cat/client.xml,此文件有OP控制,这里的Domain名字用来做开关，如果一台机器上部署了多个应用，可以指定把一个应用的监控关闭。注意这里的目录必须要有读写权限。**联系运维@夏康进行配置**

```
<?xml version="1.0" encoding="utf-8"?>
<config mode="client">
    <servers>
       <server ip="172.17.14.186" port="2280" http-port="8080" />
    </servers>
    <domain id="tms-service" enabled="true"/>
    <domain id="tms-web" enabled="true"/>
</config>
```

# 



