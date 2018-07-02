---
title: '无法删除邮箱数据库: Exchange 2013 Help'
TOCTitle: 无法删除邮箱数据库
ms:assetid: 5881e4c0-c2e2-48db-84b4-7f9ce3cf46a7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.unwillingtoremovemailboxdatabase(v=EXCHG.150)
ms:contentKeyID: 50490593
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 无法删除邮箱数据库

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2012-11-08_

Microsoft Exchange Server 2013 安装程序无法继续，因为无法在不发生潜在数据丢失的情况下从本地服务器中删除用户邮箱数据库。

在删除邮箱服务器角色之前，Exchange 2013 安装程序会确定是否从服务器中删除了所有邮箱数据库。但是，用户邮箱可能仍然保留在该服务器上。

若要解决此问题，请将服务器上的所有邮箱移动到其他 Exchange 服务器；或者，如果不再需要邮箱及其中包含的数据，请禁用邮箱。然后再次运行 Exchange 2013 安装程序。

  - 有关如何在数据库中确定邮箱的详细信息，请参阅 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))。

  - 有关如何移动邮箱的详细信息，请参阅 [Exchange 2013 中的邮箱移动](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

  - 有关如何禁用邮箱的详细信息，请参阅 [Disable-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997210\(v=exchg.150\))。

  - 有关如何删除邮箱数据库的详细信息，请参阅 [管理 Exchange 2013 中的邮箱数据库](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

