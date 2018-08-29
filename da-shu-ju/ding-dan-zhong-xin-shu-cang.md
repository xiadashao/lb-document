**各维度统计订单销售额数仓设计图（基于星型模型）**![](/assets/data2-0.png)时间维度数来源，订单表的创建时间统计业务时间的前一天格式化yyyymmdd作为主键，并通过时间格式化函数处理成年月日，定时同步到时间维度表。lb\_order 表的 create\_time 字段

代理商维度、业务员维表数据均来源erp1.0

套餐维度表  数据来源lb\_combo

客户维即购买商品的幼儿园

地域表数据来源于lb\_addr\_area



数据仓库的基本概念请参考

[http://cxy7.com/articles/2017/06/23/1498211944874.html\#b3\_solo\_h2\_15](http://cxy7.com/articles/2017/06/23/1498211944874.html#b3_solo_h2_15)

