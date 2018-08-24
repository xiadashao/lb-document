# 短信通知使用规范

1.使用位置

必需在lb-client ERP WEB端使用

2.功能实现

```
1.内控审核不通过短信通知
2.财务审核不通过短信通知
3.发货短信通知
4.结算返利短信通知
5.新增返利短信通知
```

3.短信通知对应参数

```
1.内控审核不通过
IntroControlNoPassCode
2.财务审核不通过
FinanceNoPassCode
3.发货通知
DeliverCode
4.结算返利
SettleRebateCode
5.新增返利
NewlyRebateCode

(注意)当然肯定都要传递这个用户的手机号
```

4.源码位置

![](/assets/import.png)



5.使用方式

```
  @Autowired
  AliyunSms aliyunSms;
    
  /**
   * 内容审核不通过
   * @throws Exception
   */
  public void method() throws Exception {
      //手机号
      String phone = "19800000001";
      IntroControlNoPassCode code =new IntroControlNoPassCode();
      //订单号
      code.setOrderCode("FB78666688");
      //不通过原因
      code.setRejectReason("不通过原因");
      aliyunSms.introControlNoPass(phone,code);
  }
  
  五种短信通知传递的参数都不一样,调用时根据对应的参数进行传递,实体累中都有对应的注释
```

6.使用如果出现疑问请联系

* 代码:
*       作者:张业婷
*       邮箱: zhangyeting@lbonline.cn
* 使用具体位置:
*       产品经理:郭冰冰
*       电话:188-5011-9404\(美女\)

















