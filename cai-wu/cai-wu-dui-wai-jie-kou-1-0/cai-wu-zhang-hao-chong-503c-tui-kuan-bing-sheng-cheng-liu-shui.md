### 财务账号充值/退款并生成流水

###### 业务场景：

###### 1. 代理商等通过微信给财务账户充值/代理商

###### 2.代理商等下单是微信支付后并且财务审核、内控审核不通过金额需要退回到财务账户

##### dubbo接口地址：

```
FinanceAccountService.recharge(RechargeForm rechargeForm);
```

##### 接口参数：

```
    @ApiModelProperty("账号ID")//必传
    private Long accountId;

    @ApiModelProperty("变更金额")//必传
    private Double changeAmount;


    @ApiModelProperty("凭证号码")//必传
    private String payVoucher;


    @ApiModelProperty("业务类型:1充值   6退款 ")//必传  微信充值传 1      退款传 6
    private Long businessType;

    @ApiModelProperty("支付方式：   2微信支付 ")//必传  
    private Long payType;


    @ApiModelProperty("备注")
    private String remark;

    @ApiModelProperty("修改人ID") //必传  当前登录用户
    private Long updatedId;
    @ApiModelProperty("修改人名称")//必传  当前登录用户

    private String updatedName;

    @ApiModelProperty("订单号")   //必传 
    private String orderCode;
```

##### 接口响应：

```
成功：{"code":0,"msg":"操作成功","data":null}

代理商账户不存在：{"code":-3001,"msg":"代理商财务账户不存在","data":null}
```



