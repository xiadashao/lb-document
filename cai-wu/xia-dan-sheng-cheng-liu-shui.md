### ERP/小程序下单生成流水

###### 业务场景：

###### 1. 代理商等选择余额支付，扣减财务账户余额，并生成财务流水

###### 2.代理商等下单选择线下支付或者微信支付生成财务流水

##### dubbo接口地址：

```
FinanceAccountService.handleOrder(OrderFinanceForm orderFinanceForm);
```

##### 接口参数：

```
 /**
     * 代理商财务ID
     */
    @ApiModelProperty("财务账户ID") //必填
    private Long accountId;

    /**
     * 订单号
     */
    @ApiModelProperty("订单号")//必填
    private String orderCode;

    /**
     * 金额
     */
    @ApiModelProperty("总金额")//必填
    private Double amount;

    /**
     * 支付方式
     */
    @ApiModelProperty("支付方式：  1余额支付   2微信支付  3线下支付  7欠款支付 ")//必填

    private Integer payType;

    /**
     * 支付凭证
     */
    @ApiModelProperty("支付凭证")//必填

    private String payVoucher;

    /**
     * 备注
     */
    @ApiModelProperty("备注")
    private String remark;


    @ApiModelProperty("修改人ID")//必填 当前登录用户
    private Long updatedId;
    @ApiModelProperty("修改人名称")//必填
    private String updatedName;
```

##### 响应：

```
成功：{"code":0,"msg":"操作成功","data":null}

余额不足：{"code":-3002,"msg":"余额不足，请充值","data":null}

代理商账户不存在：{"code":-3001,"msg":"代理商财务账户不存在","data":null}
```



