注释完整性：有些复杂或较长时间的代码，如无良好注释，阅读代码耗费较长时间；新人交接代码时间长，甚至新人无注释，可能理解业务逻辑错误。



注释地方：class / interface、method、代码段

例如：

```java
/**
 * 登陆服务
 * 包含用户登陆、推出、token检测
 */
public class LoginServiceImpl implements ILoginService {

/**
 * 登陆方法
 * @param accountName 用户名
 * @param userPassword 密码
 * @return 返回token
 */
public ResultVo login(String accountName, String userPassword){
 // 关键代码段
 return ;
}
```

日志重要性：线上出现偶发性问题，无法快速定位问题。同时重要数据，例如支付订单等数据出现异常，后期无法做数据补偿操作，即使人工介入无留底数据。 

建议：日志类型分为调试信息、错误信息、重要信息 

调试信息：出入参数打印 

错误信息：普通错误信息、服务异常信息 

重要信息：订单支付等重要信息 

根据信息重要程度不同，使用不同级别日志打印，新版本上线后日志级别较低，打印信息较全，易定位出现问题所在；

运行一段时间系统相对稳定后防止日志量过大，把日志级别调高。 

格式：服务IP-打印时间-服务名称-方法名称-行号-备注：哪台机器什么时间哪个类的那个方法在哪行出现了什么问题



上述部分打印参数会封装成jar包，提供使用。目前需要把日志打印全，格式在未出现jar包前可自定

