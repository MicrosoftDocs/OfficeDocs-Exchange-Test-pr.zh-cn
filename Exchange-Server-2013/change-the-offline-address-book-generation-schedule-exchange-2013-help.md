---
title: '更改脱机通讯簿生成日程安排: Exchange Online Help'
TOCTitle: 更改脱机通讯簿生成日程安排
ms:assetid: d2b4d527-311e-442d-9f1f-54fac8371b80
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124719(v=EXCHG.150)
ms:contentKeyID: 50491610
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.OfflineAddressBookGeneralPage
ms.translationtype: MT
---

# 更改脱机通讯簿生成日程安排

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-12-05_

脱机通讯簿 (OAB) 是已下载的通讯簿副本，以便 Outlook 用户在与服务器断开连接时可以访问其中所包含的信息。可以配置通过在 Set-MailboxServer cmdlet 上使用 *OABGeneratorWorkCycle* 和 *OABGeneratorWorkCycleCheckpoint* 参数生成 OAB 的频率。

有关与 OAB 相关的更多管理任务，请参阅[脱机通讯簿程序](offline-address-book-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的\&quot;脱机通讯簿\&quot;条目。

  - 您不能使用 Exchange 管理中心 (EAC) 执行此过程，必须使用 Shell。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序配置 OAB 属性

在此示例中，在邮箱服务器 MBXServer01 上每天每六小时生成一次脱机通讯簿。

    Set-MailboxServer -Identity MBXServer01 -OABGeneratorWorkCycle 01.00:00:00 -OABGeneratorWorkCycleCheckpoint 06:00:00 

有关语法和参数的详细信息，请参阅 [Set-OfflineAddressBook](https://technet.microsoft.com/zh-cn/library/aa996330\(v=exchg.150\))。

