*Amazon Simple Notification Service*
# 基本介绍
## 功能
通知服务。
一种Web服务，可从远端轻松设定、操作和发送通知。
>**解决问题：**
>可解决应用程序或基础设施中发生事件时，适当的订阅者未收到应悉知的重要消息的问题。

## 优势
- 可以直接发送消息给 200 个国家/地区的使用者。
	- 短信
	- Apple、Android和其他平台上的推送
	- 电子邮件（SMTP）
- 使用多种策略相结合，以提供消息的持久性。如果订阅的端点不可以，Amazon SNS会启动 重试消息发送 的功能。

## 如何使用 SNS 构建云端解决方案
![[imgs/Pasted image 20230810172100.png]]
图例：架构故障时发送通知
>1. 当 EC2 执行个体失败，CloudWatch 将会收到通知。
>2. CloudWatch 触发动作：
>	1. 通过  Amazon EC2 Auto Scaling 创建新的 EC2 执行个体。
>	2. 触发 Amazon SNS ，向订阅者发送通知，以便进一步调查问题。