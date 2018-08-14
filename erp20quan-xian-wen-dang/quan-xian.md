项目地址[git@code.aliyun.com:erp-server/foreverYoung.git](mailto:git@code.aliyun.com:erp-server/foreverYoung.git)user分之

主要负责的内容角色管理，账号管理，权限控制

角色管理src/components/systemSetting/jurisdiction

账号管理src/components/systemSetting/account

功能已经ok，遗留问题角色权限树的展示

权限控制：主要通过调用后台返回的权限，与前端的tabs进行匹配筛选,layout组件下有同样的逻辑

![](/assets/12121.png)

登陆权限控制：主要是通过登录后拿到token，拦截每次请求把token通过headers传递给后端，后端通过拦截校验；然后路由守卫拦截每次路由判断token是否跳转登陆页；错误路由定向到/goodslist页；权限里没有的路由会定向到权限第一个路由页面

![](/assets/23232.png)![](/assets/23231.png)

目前测试在本地测试：修改package.json npm run dev命令，加上局域网ip进行本地测试

![](/assets/23237.png)

目前所有代码已提交git；如有问题请与我联系17600452412（手机号/微信号）

