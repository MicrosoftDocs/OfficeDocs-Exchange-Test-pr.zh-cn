---
title: '数据库可移植性: Exchange 2013 Help'
TOCTitle: 数据库可移植性
ms:assetid: 387b727a-ce51-4910-b5c4-613c693fa5bd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876873(v=EXCHG.150)
ms:contentKeyID: 51408211
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 数据库可移植性

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2017-01-30_

数据库可移植性是使 Microsoft Exchange Server 2013 邮箱数据库移动到或装入同一组织中的任何其他邮箱服务器的功能，此组织运行具有相同数据数据库架构版本的数据库的 Exchange 2013。以前版本的 Exchange 的邮箱数据库无法移动到运行 Exchange 2013 的邮箱服务器。通过使用数据库可移植性，可以免除恢复过程中容易导致错误的多个手动步骤，从而提高可靠性。此外，数据库可移植性可减少各种故障情况的总恢复时间。

当使用数据库可移植性恢复邮箱数据库时，操作系统版本、源上的 Exchange Server 版本以及目标 Exchange 服务器必须相同。 例如，如果 Exchange 2013 邮箱数据库之前已装入运行 Windows Server 2012 的服务器，那么只有在将数据库迁移到同样运行 Windows Server 2012 和 Exchange 2013 的服务器上时，数据库可移植性才能正常使用。

有关如何使用数据库可移植性功能执行数据库恢复的信息，请参阅[使用数据库可移植性移动邮箱数据库](move-a-mailbox-database-using-database-portability-exchange-2013-help.md)。

