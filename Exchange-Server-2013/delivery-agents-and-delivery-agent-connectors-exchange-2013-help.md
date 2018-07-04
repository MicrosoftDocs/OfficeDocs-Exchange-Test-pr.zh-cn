---
title: '传递代理和传递代理连接器: Exchange 2013 Help'
TOCTitle: 传递代理和传递代理连接器
ms:assetid: 38c942ee-b59d-47ec-87eb-bebad441ada5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638118(v=EXCHG.150)
ms:contentKeyID: 50490322
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 传递代理和传递代理连接器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

传递代理可以从 SMTP Exchange Server 环境向不使用 SMTP 协议的系统传递邮件。每个传递代理都与一个传递代理连接器关联，该连接器会安排路由到传递代理的邮件排队等待处理，然后传递到非 SMTP 设备或系统。

> [!tip]
> 虽然外部连接器体系结构仍保留在 Microsoft Exchange 2013 中，但我们建议尽可能将传递代理用于将邮件路由到非 SMTP 系统。这样做的主要原因是，可以对邮件使用队列管理，无需管理指向投递目录的文件传输，并且可以验证邮件传递是否成功。


**目录**

传递代理的功能和优点

向组织中添加传递代理

传递代理连接器

默认的文本消息传递代理连接器

## 传递代理的功能和优点

传递代理是邮箱服务器的传输服务中安装的一个组件，可以执行下列任务：

  - 为邮件传递建立与外部系统的连接。

  - 从邮箱服务器上的传递队列中检索邮件。

  - 将邮件传递到外部系统。

  - 提供有关每次邮件成功传递的确认。

虽然外部连接器体系结构仍保留在 Microsoft Exchange Server 2013 中，但我们建议尽可能将传递代理用于将邮件路由到非 SMTP 系统。传递代理具有下列优点：

  - 允许对路由到外部系统的邮件进行队列管理。

  - 因为邮件不再需要写入到文件系统和从文件系统中进行读取，所以邮件传递性能得到了提高。

  - 为代理开发人员提供了对包含丰富事件的邮件属性的访问权限。

  - 传递代理的开发时间比实施外部连接器所需的时间短，因为传递代理可以使用 Exchange 的邮件表示和管理功能。

  - 您可以验证邮件是否已传递到外部系统，而不是简单地写入投递目录。

  - 使用传递代理连接器能够进行服务级别协议 (SLA) 分析，因为这样可以跟踪到外部系统的邮件传递延迟情况。

## 向组织中添加传递代理

若要在组织中使用传递代理，必须完成以下操作：

1.  获取传递代理。通常，传递代理由第三方编写。Exchange 2013 在默认情况下仅附带一个传递代理连接器：文本消息传递代理连接器。

2.  在即将为传递代理连接器充当源服务器的邮箱服务器的传输服务中安装传递代理。

3.  针对特定协议创建传递代理连接器。

完成所有这些步骤后，发往外部系统的邮件将通过传递代理连接器进行路由，并由传递代理进行处理。

[Microsoft.Exchange.Data.Transport.Delivery Namespace](https://go.microsoft.com/fwlink/?linkid=262690) 提供了有关开发传递代理的详细信息。

## 传递代理连接器

Exchange 2013 中的传递代理连接器与 Exchange 2010 中引入的传递代理连接器类似。它们根据地址将邮件路由到不使用 SMTP 协议的外部系统。当邮件路由到传递代理连接器时，相关的传递代理将执行内容转换和邮件传递。通常，传递代理由第三方创建，并配置为与您组织中的传递代理连接器配合使用。

您不能在 Exchange 管理中心内创建传递代理连接器，而要在 Exchange 命令行管理程序中使用 [New-DeliveryAgentConnector](https://technet.microsoft.com/zh-cn/library/dd351063\(v=exchg.150\)) cmdlet 进行创建，然后使用 [Set-DeliveryAgentConnector](https://technet.microsoft.com/zh-cn/library/dd351159\(v=exchg.150\)) 编辑传递代理连接器的属性。您可以使用可选的 *SourceTransportServers* 参数，为该连接器指定一个或多个主机邮箱服务器。

## 默认的文本消息传递代理连接器

您可以使用文本消息传递代理连接器将邮件路由到移动设备。在 Exchange 服务器上，运行 `Get-DeliveryAgentConnector | fl` 以查看连接器及其所有参数。请注意，*DeliveryProtocol* 设置为 `MOBILE`。

