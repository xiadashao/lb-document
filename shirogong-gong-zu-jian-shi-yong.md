# web服务集成shiro

## 1. 项目加入依赖的jar包

```
       <dependency>
    <groupId>com.lbonline</groupId>
    <artifactId>lbonline-shiro-spring-boot-starter</artifactId>
    <version>1.0.0.RELEASE</version>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </exclusion>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </exclusion>
        <exclusion>
            <groupId>com.alibaba.spring.boot</groupId>
            <artifactId>dubbo-spring-boot-starter</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

## 2. 引用用户dubbo服务

```
@Component
public class ShiroConfig {

    @Reference(version = "1.0.0")
    private ILoginService loginService;

    @Bean(name = "iLoginService")
    public  ILoginService getLoginService() {
        return  loginService;
    }

}
```

###  3.application.yml配置

如下例:

```
shiro:
  secret: lb-shiro-jwt//密钥
  expire-time: 43200000//失效时间
  no-authorized-definitions://不走jwt拦截器
    - key: /swagger-resources/**
      value: anon
    - key: /webjars/**
      value: anon
    - key: /swagger-ui.html
      value: anon
    - key: /v2/api-docs/**
      value: anon
  perms-filter-definitions://url需要做权限过滤的需要自己扩展
    - key: /api/config/product/list
      value: jwt,perms[/api/config/product/list]
    - key: /api/salesUnit/salesUnitList
      value: jwt,perms[/api/salesUnit/salesUnitList]
    - key: /api/config/combo/list
      value: jwt,perms[/api/config/combo/list]
    - key: /api/config/product/type
      value: jwt,perms[/api/config/product/type]
    - key: /api/config/product/class
      value: jwt,perms[/api/config/product/class]
    - key: /api/config/project/type
      value: jwt,perms[/api/config/project/type]
    - key: /api/customForm/list
      value: jwt,perms[/api/customForm/list]
    - key: /api/orderManagement/list
      value: jwt,perms[/api/orderManagement/list]
    - key: /api/order
      value: jwt,perms[/api/order]
    - key: /api/orderManagement/list
      value: jwt,perms[/api/orderManagement/list]
    - key: /api/sendGoods/list
      value: jwt,perms[/api/sendGoods/list]
    - key: /api/stockOut/list
      value: jwt,perms[/api/stockOut/list]
    - key: /api/carriage/list
      value: jwt,perms[/api/carriage/list]
    - key: /api/work/findHardwareList
      value: jwt,perms[/api/work/findHardwareList]
    - key: /api/work/findNetWorkList
      value: jwt,perms[/api/work/findNetWorkList]
    - key: /api/work/findNetWorkReportList
      value: jwt,perms[/api/work/findNetWorkReportList]
    - key: /api/financeAccount/list
      value: jwt,perms[/api/financeAccount/list]
    - key: /api/financeAccount/list
      value: jwt,perms[/api/financeAccount/list]
    - key: /api/debts/list
      value: jwt,perms[/api/debts/list]
    - key: /api/accountStream/list
      value: jwt,perms[/api/accountStream/list]
    - key: /api/rebate/listPreRebate
      value: jwt,perms[/api/rebate/listPreRebate]
    - key: /api/rebate/listRebate
      value: jwt,perms[/api/rebate/listRebate]
    - key: /api/rebate/listAlreadyRebate
      value: jwt,perms[/api/rebate/listAlreadyRebate]
    - key: /api/user/list
      value: jwt,perms[/api/user/list]
    - key: /api/role/list
      value: jwt,perms[/api/role/list]
    - key: /api/menu/list
      value: jwt,perms[/api/menu/view]
```

### 4.动态菜单

```
  @Reference(version = "1.0.0",timeout = 50000)
    private IMenuService menuService;

    @GetMapping("/view")
    @ApiOperation(value = "动态权限", notes = "动态权限")
    public ResultVo findMenuDetail()
    {
        return menuService.findMenuDetail(UserInfoUtil.getUserInfo().getUserId());
    }
```

### 5.获取用户信息

```
UserVo user = UserInfoUtil.getUserInfo();
```

### 6.页面请求需要在header中携带token



