---
title: 'SMTP 地址格式不 Supported_SMTPAddressLiteral: Exchange 2013 Help'
TOCTitle: SMTP 地址格式不 Supported_SMTPAddressLiteral
ms:assetid: b8b55917-d81f-4c0a-ad65-7bb10ac58df8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.smtpaddressliteral(v=EXCHG.150)
ms:contentKeyID: 50491414
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# SMTP 地址格式不 Supported\_SMTPAddressLiteral

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为指定的收件人策略使用不支持的简单邮件传输协议 (SMTP) 地址格式，所以 Microsoft Exchange Server 2007 和 Exchange Server 2010 安装程序无法继续进行。

Exchange 2007 和 Exchange 2010 安装程序需要的所有 SMTP 地址用于电子邮件地址策略不都包含 IP 地址字符串，例如︰ *user@\[10.10.1.1\]*。

要解决此问题，请更改收件人策略中的 SMTP 地址的值，以便它不包含 IP 地址文本。方括号 (\[\]) 和替换文本的 IP 地址 (10.10.1.1) 号的域名系统 (DNS) 命名格式，例如︰ *user@contoso.com*，然后重新运行 Exchange 安装程序。

有关管理 Exchange Server 2007年中的收件人策略的详细信息，请参阅"管理电子邮件地址策略"([https://go.microsoft.com/fwlink/?LinkId=86653](https://go.microsoft.com/fwlink/?linkid=86653))。

有关管理 Exchange Server 2010年中的收件人策略的详细信息，请参阅"管理电子邮件地址策略"([https://go.microsoft.com/fwlink/?LinkId=179519](https://go.microsoft.com/fwlink/?linkid=179519))。

