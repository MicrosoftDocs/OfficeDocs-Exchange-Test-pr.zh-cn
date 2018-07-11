---
title: '边缘传输服务器上的收件人筛选: Exchange 2013 Help'
TOCTitle: 边缘传输服务器上的收件人筛选
ms:assetid: 994eefd9-3903-41e6-a882-1e333d6d2d18
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123891(v=EXCHG.150)
ms:contentKeyID: 50491128
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 边缘传输服务器上的收件人筛选

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-05-07_

收件人筛选是 Microsoft Exchange Server 2013 中的\&quot;反垃圾邮件功能\&quot;，根据 RCPT TO SMTP 头确定对入站邮件执行哪些操作（如果有）。收件人筛选由收件人筛选器代理执行。

收件人筛选器代理根据组织内预期收件人的特征来阻止邮件。在下列方案中的收件人筛选器代理有助于阻止邮件的接收：

  - **不存在的收件人**   可以阻止向不在组织通讯簿中的收件人传递邮件。例如，可以阻止向常被误用的帐户名称（如 administrator@contoso.com 或 support@contoso.com）传递邮件。

  - **受限制的通讯组列表**   可以阻止向仅由内部用户使用的通讯组列表传递 Internet 邮件。

  - **从不接收 Internet 邮件的邮箱**   可以阻止向通常仅在组织内部使用的特定邮箱或别名（例如 Helpdesk）传递 Internet 邮件。

收件人筛选器代理对存储在下列数据源之一或两者中的收件人执行操作：

  - **收件人阻止列表**   由管理员定义的，从不接收 Internet 邮件的收件人列表。

  - **收件人查找**   查询 Active Directory 以验证组织中存在收件人。在边缘传输服务器上，收件人查找需要访问 EdgeSync 提供的 Active Directory 信息，以获取 Active Directory 轻型目录服务（AD LDS）的本地实例。

在启用了收件人筛选器代理后，系统将根据收件人的特征，对入站邮件执行下列操作之一。这些收件人由 RCPT TO 头表示。

  - 如果入站邮件包含收件人阻止列表中的收件人，则 Exchange 服务器会向发送服务器发送 `550 5.1.1 User unknown` SMTP 会话错误。

  - 如果入站邮件包含与收件人查找中的任何收件人不匹配的收件人，则 Exchange 服务器会向发送服务器发送 `550 5.1.1 User unknown` SMTP 会话错误。

  - 如果收件人不在收件人阻止列表而在收件人查找中，则 Exchange 服务器会向发送服务器发送 `250 2.1.5 Recipient OK` SMTP 响应，本链中的下一个反垃圾邮件代理将处理该邮件。

**目录**

Configuring recipient lookup

Tarpitting functionality

Multiple namespaces

## 配置收件人查找

减少垃圾邮件的一种最有效的方法是在接受来自 Internet 的入站邮件之前验证收件人。在 Exchange 命令行管理程序中使用 **Set-RecipientFilterConfig** cmdlet，您可以阻止向 Exchange 组织中不存在的收件人发送邮件，还可以阻止特定的收件人。有关详细信息，请参阅[管理边缘传输服务器上的收件人筛选](manage-recipient-filtering-on-edge-transport-servers-exchange-2013-help.md)。

如果外围网络中安装有边缘传输服务器，最好配置在边缘传输服务器上运行的 AD LDS 实例，以与 Active Directory 保持同步。默认情况下，在边缘传输服务器上安装和配置 AD LDS。但是，您必须配置 AD LDS，通过订阅您组织的边缘传输服务器与 Active Directory 加入域的全局目录服务器进行通信。有关详细信息，请参阅[在 Exchange 2013 中使用 Exchange 2010 或 2007 边缘传输服务器](use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md)。

返回顶部

## 缓送技术功能

收件人查找功能可让发送服务器决定电子邮件地址有效还是无效。如上所述，当入站邮件的收件人是已知收件人时，Exchange 服务器会向发送服务器发送回 `250 2.1.5 Recipient OK` SMTP 响应。此功能为帐户搜集攻击提供了一个理想的环境。

\&quot;帐户搜集攻击\&quot;是试图从特定组织收集有效的电子邮件地址，以便将这些电子邮件地址添加到垃圾邮件数据库的一种行为。因为所有的垃圾邮件收入均依赖于试图使人们打开电子邮件，因此处于活动状态的地址是恶意用户或*垃圾邮件制造者*从中获得利益的商品。因为 SMTP 协议对已知发件人和未知发件人提供反馈，所以垃圾邮件制造者可以编写一个自动程序，使用常见名称或字典词汇组成特定域的电子邮件地址。该程序会收集返回 `250 2.1.5 Recipient OK` SMTP 响应的所有电子邮件地址，并丢弃返回 `550 5.1.1 User unknown` SMTP 会话错误的所有电子邮件地址。垃圾邮件制造者随后出售这些有效的电子邮件地址或将其用作未经请求的邮件的收件人。

为了预防帐户搜集攻击，Exchange 2013 包括了缓送技术功能。\&quot;缓送技术\&quot;是针对表明有大量垃圾邮件或其他不受欢迎邮件的特定 SMTP 通信模式，人工延迟服务器响应的一种方法。缓送技术的目的是减慢此类电子邮件通信的通信过程，从而增加发送垃圾邮件的组织和个人发送垃圾邮件的成本。缓送技术使帐户搜集攻击变得非常昂贵以至于无法有效地自动进行。

如果没有配置缓送技术，当在收件人查找中没有找到收件人时，Exchange 服务器会立即向发件人返回 `550 5.1.1 User unknown` SMTP 会话错误。然而，如果配置了缓送技术，SMTP 在返回 `550 5.1.1 User unknown` 错误前会等待指定的秒数。SMTP 会话中的这种暂停会使自动进行的帐户搜集攻击变得更加困难，从而降低垃圾邮件制造者的成本效益。默认情况下，接收连接器的缓送技术配置为 5 秒。

若要在 SMTP 返回 `550 5.1.1 User unknown` 错误前配置延迟，请在 **Set-ReceiveConnector** cmdlet 上使用 *TarpitInterval* 参数设置缓送间隔。语法是：

    Set-ReceiveConnector <Receive Connector> -TarpitInterval <00:00:00 to 00:10:00>

默认值是 `00:00:05` 或 5 秒。边缘传输服务器上默认接收连接器的名称为 `Default internal receive connector <server name>`。

决定更改缓送间隔时必须谨慎。如果间隔太长，会中断正常的邮件流；但是如果间隔太短，在阻止帐户搜集攻击时又不能发挥预期作用。如果更改缓送间隔，请逐步少量地进行并验证结果。例如，如果 5 秒钟无效，请尝试将间隔更改为 10 秒。

返回顶部

## 多个命名空间

收件人筛选器代理仅为权威域执行收件人查找。如果您的组织代表配置为内部中继域或外部中继域的另一个域接受和转发邮件，则收件人筛选器代理不会对这些域中的收件人执行收件人查找。但是，如果收件人阻止列表中指定收件人，收件人筛选器代理仍然会阻止该收件人。

请注意，您还可以在边缘传输服务器本地配置接受域。如果域配置为内部中继域或外部中继域，则边缘传输服务器上的收件人筛选器代理也不会对这些域中的收件人执行收件人查找。

返回顶部

