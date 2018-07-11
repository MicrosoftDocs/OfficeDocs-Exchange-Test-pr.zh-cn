---
title: '移动设备: Exchange 2013 Help'
TOCTitle: 移动设备
ms:assetid: 93a949e7-b3ef-43ea-ae0c-6698826fc8d2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232129(v=EXCHG.150)
ms:contentKeyID: 50491189
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 移动设备

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-09-24_

用户可通过启用了 MicrosoftExchange ActiveSync 的移动设备随时随地访问其大部分 Microsoft Exchange 邮箱数据。很多不同的移动电话和移动设备都启用了 Exchange ActiveSync。这些设备包括 Windows Phone、Nokia 移动电话、Android 电话和平板电脑、Apple iPhone、iPod 和 iPad。

尽管电话和非电话移动设备都支持 Exchange ActiveSync，但在大多数 Exchange ActiveSync 文档中，我们使用*移动设备*这一术语。除非我们讨论的功能需要移动电话信号（如 SMS 消息通知），否则术语“移动设备”同时适用于移动电话和其他移动设备（如平板电脑）。

## Exchange ActiveSync

Exchange ActiveSync 是一个通信协议，它允许用户通过无线方式移动访问电子邮件、调度数据、联系人和任务。在 Windows Phone 和启用了 Exchange ActiveSync 的第三方电话上，可以使用 Exchange ActiveSync。

Exchange ActiveSync 提供直推技术。直推技术使用移动设备与服务器之间建立并保持的加密 HTTPS 连接，将新的电子邮件和其他 Exchange 数据推送到电话上。

要将直推技术用于 MicrosoftExchange Server 2013，用户必须具备支持直推技术的移动设备。

## Exchange ActiveSync 功能

Exchange ActiveSync 让您可以访问许多不同的功能，借助这些功能，您可以在移动设备上强制执行安全策略。使用 Exchange 2013，您可以配置多个移动设备邮箱策略，并控制哪些移动设备可以与 Exchange 服务器同步。Exchange ActiveSync 让您能够发送远程设备擦除命令，当移动设备丢失或被盗时，可以擦除上面的所有数据。用户也可以从 Outlook Web App 启动远程设备擦除。

Exchange ActiveSync 使用户可以生成恢复密码。此恢复密码保存在移动设备上，供用户忘记密码时使用。用户在生成设备密码或 PIN 的同时生成恢复密码。此恢复密码可用于解锁移动设备。使用了此恢复密码后，将立即要求用户创建一个新 PIN。

## POP3 和 IMAP4

如果您的移动设备不支持 Exchange ActiveSync，或者您不需要 Exchange ActiveSync 提供的丰富功能集，可以在移动设备上使用 POP3 或 IMAP4 访问电子邮件。有关使用 POP3 和 IMAP4 访问邮箱的详细信息，请参阅 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

