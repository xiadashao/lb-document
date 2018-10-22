# 消息服务使用规范

## 一.功能简介

1.支持短信、邮件、微信小程序、站内信4种消息类型.

2.支持实时、定时2种发送类型.

3.支持统一的调用入口.

## 二.使用说明

```
<groupId>com.lbonline</groupId>
<artifactId>lb-message-api</artifactId>
<version>0.0.1-SNAPSHOT</version>
```

## 三.api

```
/**
* 发送消息通知
* @param params 消息内容,json格式
* @return
*/
public ResultVo sendMessage(String params);

/**
 * 根据查询条件获取站内信信息
 * @param letterDto 站内信查询条件
 * @return
 */
public ResultVo findLetters(LetterDto letterDto);

/**
 * 根据条件更新站内信信息
 * @param letterDto 站内信更新条件
 * @return
 */
public ResultVo updateLetter(LetterDto letterDto);

/**
 * 创建微信用户表单
 * @param openFormMappingDto 微信用户关系
 * @return
 */
public ResultVo addOpenFormMapping(OpenFormMappingDto openFormMappingDto);
```

## 四.参数说明

1.发送短信

| 字段 | 类型 | 是否必填 | 备注 |
| :--- | :--- | :--- | :--- |
| messageType | Byte | 是 | 消息类型:1短信2邮件3微信小程序4站内信 |
| fromEnd | Byte | 是 | 发送端 TODO |
| businessType | Byte | 是 | 业务类型 TODO |
| smsSign | String | 是 | 短信签名 |
| templateId | String | 是 | 模板id |
| to | String | 是 | 接收人手机号 |
| content | String | 否 | 短信模板内容 |

2.发送邮件

| 字段 | 类型 | 是否必填 | 备注 |
| :--- | :--- | :--- | :--- |
| messageType | Byte | 是 | 消息类型:1短信2邮件3微信小程序4站内信 |
| fromEnd | Byte | 是 | 发送端 TODO |
| businessType | Byte | 是 | 业务类型 TODO |
| subject | String | 是 | 邮件主题 |
| to | String | 是 | 收件人地址 |
| content | String | 是 | 邮件内容 |

3.发送微信小程序通知

| 字段 | 类型 | 是否必填 | 备注 |
| :--- | :--- | :--- | :--- |
| messageType | Byte | 是 | 消息类型:1短信2邮件3微信小程序4站内信 |
| fromEnd | Byte | 是 | 发送端 TODO |
| businessType | Byte | 是 | 业务类型 TODO |
| to | String | 是 | openId |
| content | String | 否 | 通知内容 |
| accessToken | String | 是 | access\_toke |
| userId | String | 是 | 用户id |
| page | String | 否 | 小程序模板是否跳转 |
| color | String | 否 | 小程序模板颜色,默认黑色 |
| emphasis | String | 否 | 小程序关键词是否放大,默认否 |

4.发送站内信

| 字段 | 类型 | 是否必填 | 备注 |
| :--- | :--- | :--- | :--- |
| messageType | Byte | 是 | 消息类型:1短信2邮件3微信小程序4站内信 |
| fromEnd | Byte | 是 | 发送端 TODO |
| businessType | Byte | 是 | 业务类型 TODO |
| to | String | 是 | 信息接收人 |
| toEnd | Byte | 是 | 接收端 TODO |
| content | String | 是 | 消息内容 |
| letterType | Byte | 是 | 站内信消息类型:1互动消息2作业消息3系统消息 |

5.其他字段

| 字段 | 类型 | 是否必填 | 备注 |
| :--- | :--- | :--- | :--- |
| sendType | Byte | 否 | 发送类型:1实时2定时,默认实时 |
| timeStamp | Long | 否 | 定时发送具体时间戳,默认0L |

## 五.后期迭代

1.确定发送端、接收端、业务类型的具体信息.

2.短信邮件批量发送数限制,分批发送至mq.

3.邮件丰富模板发送,附件发送.

4.增加日志记录.





