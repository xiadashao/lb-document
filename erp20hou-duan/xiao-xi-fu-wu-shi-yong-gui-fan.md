消息服务使用规范

一.功能简介

1.支持短信、邮件、微信小程序、站内信4种消息类型.



2.支持实时、定时2种发送类型.



3.支持统一的调用入口.



二.使用说明

&lt;groupId&gt;com.lbonline&lt;/groupId&gt;

&lt;artifactId&gt;lb-message-api&lt;/artifactId&gt;

&lt;version&gt;0.0.1-SNAPSHOT&lt;/version&gt;

三.api

/\*\*

 \* 发送消息通知

 \* @param params 消息内容,json格式

 \* @return

 \*/

public ResultVo sendMessage\(String params\);

四.参数说明

