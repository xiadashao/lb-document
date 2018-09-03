### 分期支付生成欠款

###### 业务场景：

###### 线下支付,微信支付或余额支付，如果选择分期只支付首期款，剩下的分期在审核通过后调用财务接口生成欠款

##### dubbo接口地址：

```
FinanceAccountService.createDebts(OrderDebtsHeadForm orderDebtsHeadForm);
```

##### 接口参数：

```
     @ApiModelProperty("财务账户ID")//必填
    private Long accountId;

    @ApiModelProperty("订单号")//必填

    private String orderCode;

    @ApiModelProperty("修改人ID")//必填

    private Long updatedId;

    @ApiModelProperty("修改人名称")//必填

    private String updatedName;

    /*** 分期列表（首次只支付首期款,然后分期二期，三期等按照顺序保存）
     */
    @ApiModelProperty("分期列表明细(从第二期开始算)")//必填

    List<OrderDebtsDetailForm> hirePurchaseList;
    {

         @ApiModelProperty("欠款方: 1 代理商   2 园所")//必填


         private Integer debtPart;


         @ApiModelProperty("园所名称（园所必填）")
         private String kindergarten;


         @ApiModelProperty("款项名称(欠款必填 例如 D55D65二期应收)")//必填


         private String moneyArticle;


         @ApiModelProperty("分期金额")//必填


         private Double hpAmount;


         @ApiModelProperty("园所电话（园所必填）")
         private String kindergartenTel;

         @ApiModelProperty("预计还款时间")//必填


         @DateTimeFormat(pattern="yyyy-MM-dd")
         private Date planRepayTime;
    }
```

##### 响应：

```
成功：{"code":0,"msg":"操作成功","data":null}

代理商账户不存在：{"code":-3001,"msg":"代理商财务账户不存在","data":null}
```



