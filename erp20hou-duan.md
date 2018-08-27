### 1.认证

因项目使用soa服务架构,认证处理思路:采用redis进行分布式session管理

* 登陆信息校验,生成token,将token及user info以key-value形式存入redis中缓存,返回token.

* token校验,前端以请求头的形式传递token,后端校验token,返回用户id,用户名称,角色信息,权限信息.

注意:lb-client、lb-user需采用相同的redis配置.

### 2.鉴权

因项目采用前后端分离技术,鉴权处理思路:由前端进行功能权限的维护

* 前端根据token校验返回的用户权限信息进行功能权限的展示,具体实现实现可参考:ERP2.0权限文档.

* 后端实现:

1. 引入pom依赖

    ![](/assets/shiro-pom.png)

   2.编写shiro的配置类ShiroConfiguration,进行定义shiro过滤器,同时自定义认证过滤,权限过滤器,用于用户认证,鉴权过滤.具体事项可参考:lb-online-platform项目的lb-client模块中的ShiroConfiguration配置类,LbUserAuthFilter认证过滤器,LbUserPermFilter权限过滤器.



