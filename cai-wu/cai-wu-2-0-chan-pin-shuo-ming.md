## 概述

财务主要管理客户在我公司的账户、流水、欠款、返利；配合各业务方提供修改余额，增减欠款，增加流水的服务。

公司的客户包括，代理商、园所、家庭，目前只有代理商。

## 涉及到人员

后台开发：王飞、韩录；前端开发：金涛；测试：李超；

财务主管：王辉；财务代办：刘新；市场主管：王雪艳

## 财务账户

目前只有代理商财务账户，财务账户分可用账户、不可用账户、欠款账户三个子账户。

**可用账户**

可用账户中的余额，代理商可以用来购买套餐。

可用账户的余额来源：签合同时交预付款、小程序充值、线上付款审核驳回的充值、返利充值。

**不可用账户**

不可用账户中的余额，只有申请转到可用余额，才可以使用。

不可用账户的余额来源，都是老数据，目前业务没有新增不可用账户的余额。

**欠款账户**

欠款账户中的余额，为用户的欠款。

欠款账户的余额来源：除了老数据的借款和二期款外，新增的欠款有套餐的二期款和D88盒子的免费领取。

还款途径：1、在欠款还款列表，可以直接还款，只有财务代办-fi权限的用户可以操作还款。

2、返利申请时，可以选择返利金额还欠款。

## 欠款管理

财务账户的所有欠款记录，都会在欠款管理中显示，欠款管理可以还欠款，查看还款记录。还款的操作，只有财务代办-fi权限的用户可以操作。

## 返利管理

代理商代理联帮的套餐，卖出去会给返利奖励，返利规则详见《820财务规则》文档。

返利由渠道运营的同事来申请，申请时可以选择返利金额提现or充值，也可以选择返利金额是否还款，具体还哪些款项，申请提交后，经过层层审核，最终到达财务代办，财务代办可以打款，完成返利申请，也可以驳回，驳回后返利申请由当初的申请人重新申请。

返利申请审核的步骤：

1、返利申请，【渠道运营-财务】权限可以操作（渠道运营所有人员）

2、待渠道主管审核状态的返利申请，【返利审核-渠道主管】权限可以操作审核（杨琴）

3、待市场审核状态的返利申请，【返利审核-市场主管】权限可以操作审核（王雪艳）

4、待内控审核状态的返利申请，【返利审核-内控专员】权限可以操作审核（熊志伟）

5、待仓库审核状态的返利申请，【返利审核-仓库主管】权限可以操作审核（张肖丽）

6、待财务审核状态的返利申请，【返利审核-财务主管】权限可以操作审核 （王辉）

7、待CEO审核状态的返利申请，【返利审核-CEO】权限可以操作审核（李白）

8、待代办打款状态的返利申请，【财务代办-fi】权限可以操作打款和拒绝打款（刘新）

9、待渠道重新申请状态的返利申请，返利申请人 可以操作重新申请

## 财务账户流水

财务账户任何的金额变动都会产生流水。

流水的业务类型包括：下单、下单-其他渠道、充值、预付款、押金、返利、退款、转账、还款、权益金。

支付方式包括：余额支付、微信支付、线下支付、余额转入、余额转出、返利支付、退款支付。

目前还没有退款功能，所以没有退款流水。

## 常见问题以及特别关注点：

1、代理商账户余额不准确，业务部门会统计好，我们来改数据

2、订单和财务的交互，一定要双方明确订单在什么情况下调用财务的接口（生成流水、修改余额、生成欠款），详细业务见财务--财务与订单交互

## 返利规则：

![](/assets/返利规则 %281%29.png)



