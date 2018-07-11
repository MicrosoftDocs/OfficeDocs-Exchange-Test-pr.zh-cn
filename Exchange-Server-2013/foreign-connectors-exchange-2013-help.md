---
title: '外部连接器: Exchange 2013 Help'
TOCTitle: 外部连接器
ms:assetid: 21c6a7a9-f4d2-4359-9ac9-930701b63a4e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996779(v=EXCHG.150)
ms:contentKeyID: 50490060
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 外部连接器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-09-25_

外部连接器将邮件传递到不使用 SMTP 作为其主传输机制的服务器或外部系统。传真-网关服务器即是这样一个示例。外部连接器使用本地或共享的删除目录通过文件传输将出站邮件发送到外部系统。外部连接器是在 Microsoft Exchange Server 2013 邮箱服务器的传输服务中创建的。

外部网关服务器可以通过使用存在于邮箱服务器传输服务中的分拣目录或重播目录将邮件发送到 Exchange 2013 组织。提交您复制到每个目录的格式正确的电子邮件文件，以传递到 Exchange 邮箱。

> [!TIP]  
> 在必须将出站邮件发送到非 SMTP 系统中的大多数情况下，我们建议使用“传递代理”连接器，因为这些连接器可以对邮件队列进行管理，邮件不必写入到文件系统中，并且还有其他优势。<a href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">传递代理和传递代理连接器</a>主题提供了更多详细信息。


## 详细信息

[创建外部连接器将邮件发送至非 SMTP 传真网关](create-a-foreign-connector-to-deliver-messages-to-a-non-smtp-fax-gateway-exchange-2013-help.md)

[传递代理和传递代理连接器](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

[New-ForeignConnector](https://technet.microsoft.com/zh-cn/library/aa996310\(v=exchg.150\))

[Set-ForeignConnector](https://technet.microsoft.com/zh-cn/library/bb123789\(v=exchg.150\))

