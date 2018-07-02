---
title: '邮箱数据库副本: Exchange 2013 Help'
TOCTitle: 邮箱数据库副本
ms:assetid: ce748bca-3e24-493b-b9e6-153157bffd6a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd979802(v=EXCHG.150)
ms:contentKeyID: 50491568
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 邮箱数据库副本

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

Microsoft Exchange Server 2013 利用了数据库移动性这一概念，它是 Exchange 托管的数据库级故障转移。数据库移动性将数据库从服务器断开，增加了对单一数据库的支持，最多可以支持 16 个副本，并提供将数据库副本添加到数据库的本机体验。

## 关键特征

邮箱数据库副本的关键特征为：

  - 可以多个邮箱服务器上最多创建 Exchange 2013 邮箱数据库的 16 个副本，只要这些服务器分组到数据库可用性组 (DAG)，这是连续复制的边界。Exchange 2013 邮箱数据库可以仅复制到 DAG 中的其他 Exchange 2013 邮箱服务器。您不能将一个数据库复制到 DAG 外部，也不能将 Exchange 2013 邮箱数据库复制到正在运行 Exchange 2010 或更早版本的服务器上。有关部署 DAG 的详细信息，请参阅[数据库可用性组 (DAG)](database-availability-groups-dags-exchange-2013-help.md)。

  - DAG 中的所有邮箱服务器必须处于相同的 Active Directory 域中。

  - 邮箱数据库副本支持重播延迟时间和截断延迟时间的概念。在启用这些功能之前，必须执行适当的规划。

  - 使用可感知 Exchange 且基于卷影复制服务 (VSS) 的备份复制可备份所有数据库副本。

  - 只能在未托管数据库的主动副本的邮箱服务器上创建数据库副本。不能在同一服务器上创建同一数据库的两个副本。

  - 数据库的所有副本在包含副本的每个服务器上使用相同的路径。每个邮箱服务器上的数据库副本的数据库和日志文件路径不得与任何其他数据库路径冲突。

  - 可以在相同或不同 Active Directory 站点中创建数据库副本，以及在相同或不同网络子网中创建数据库副本。

  - 往返网络延迟大于 500 毫秒 (ms) 的邮箱服务器之间不支持数据库副本。

## 邮箱数据库副本

您可以随时创建邮箱数据库副本。邮箱数据库副本可按照灵活精细的方式分布到邮箱服务器中。

您可以在 Exchange 管理中心中使用\&quot;添加邮箱数据库副本\&quot;向导，或在 Exchange 命令行管理程序中使用 **Add-MailboxDatabaseCopy** cmdlet 来创建邮箱数据库副本。

创建邮箱数据库副本时，请指定以下参数：

  - *Identity* 此参数指定要复制的数据库的名称。数据库名称必须在 Exchange 组织中是唯一的。

  - *MailboxServer*   此参数指定将托管数据库副本的邮箱服务器的名称。此服务器必须是同一 DAG 的成员，并且不得已托管数据库的副本。

或者，您还可以指定：

  - *ActivationPreference* 该参数指定用作活动管理器的最佳副本选择进程一部分的激活首选项编号。还可在使用 RedistributeActiveDatabases.ps1 脚本时，用于在 DAG 中重新分布主动邮箱数据库。激活首选项的值为等于或大于 1 的数字，1 表示优先顺序最高。位置编号不能大于邮箱数据库的副本数。

  - *ReplayLagTime * 此参数指定 Microsoft Exchange 复制服务在重播被复制到数据库副本的日志文件之前应等待的时间。此参数的格式为（天数.小时数:分钟数:秒数）。此参数的默认设置是 0 秒。此参数允许的最大设置是 14 天。允许的最低设置是 0 秒。如果将重播延迟时间的值设置为 0，则将关闭日志重播延迟。

  - *TruncationLagTime* 此参数指定 Microsoft Exchange 复制服务在截断被重播到数据库副本的日志文件之前应等待的时间。此时段是从日志成功地重播到数据库副本中后开始的。此参数的格式为（天数.小时数:分钟数:秒数）。此参数的默认设置是 0 秒。此参数允许的最大设置是 14 天。允许的最低设置是 0 秒。如果将截断延迟时间的值设置为 0，则将关闭日志截断延迟。

  - *SeedingPostponed* 该参数指定任务不应在指定的邮箱服务器上自动为数据库副本设定种子。若要使用现有的被动数据库副本为新的邮箱数据库副本设定种子（如，向远程位置添加特定数据库的第二个副本），通常使用该选项。使用该参数时，必须使用 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 手动为数据库副本设定种子。

有关创建、使用和管理邮箱数据库副本的详细信息，请参阅[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)。

