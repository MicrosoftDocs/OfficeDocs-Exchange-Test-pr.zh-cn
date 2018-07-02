---
title: '配置邮箱数据库副本属性: Exchange 2013 Help'
TOCTitle: 配置邮箱数据库副本属性
ms:assetid: cf186561-ab2c-45c0-90f5-8d3ecfabeeac
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351151(v=EXCHG.150)
ms:contentKeyID: 50491712
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置邮箱数据库副本属性

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-01_

每个邮箱数据库副本都有自己的属性，可供你配置。这些属性包括重播延隔时间和截断延隔时间（如果有），以及激活首选项编号。有关重播延隔时间、截断延隔时间和激活首选项编号的详细信息，请参阅[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;邮箱数据库副本\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用 EAC 配置邮箱数据库副本属性

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库\&quot;。

2.  选择要配置的数据库。

3.  在\&quot;详细信息\&quot;窗格中的\&quot;数据库副本\&quot;下，单击所需数据库副本的\&quot;查看详情\&quot;，然后查看或配置以下项目：
    
      - \&quot;数据库\&quot;   显示所选数据库的名称。
    
      - \&quot;邮箱服务器\&quot; 显示托管选定数据库副本的邮箱服务器名称。
    
      - \&quot;内容索引状态\&quot; 显示选定数据库副本的当前内容索引状态。
    
      - \&quot;状态\&quot; 显示选定数据库副本的当前状态。
    
      - **复制队列长度**   指明正在等待复制到选定数据库副本的日志文件的数量。此字段仅与被动数据库副本相关。
    
      - **重播队列长度**   指明正在等待重播到选定数据库副本的日志文件的数量。此字段仅与被动数据库副本相关。
    
      - **错误消息**   显示状态为 `Failed` 或 `Failed and Suspended` 的数据库副本的任何错误消息。
    
      - **最新可用日志时间**   显示数据库主动副本上最近一次生成的日志文件的日期和时间戳。此字段仅与被动数据库副本相关。在主动数据库副本（已复制和独立）上，此字段显示\&quot;**从不**\&quot;。
    
      - **上次检查日志的时间**   显示 LogInspector 上次在选定数据库副本上检查日志文件的日期和时间戳。此字段仅与被动数据库副本相关。在主动数据库副本（已复制和独立）上，此字段显示\&quot;**从不**\&quot;。
    
      - **上次复制日志的时间**   显示 LogCopier 上次在选定数据库副本上复制日志文件的日期和时间戳。此字段仅与被动数据库副本相关。在主动数据库副本（已复制和独立）上，此字段显示\&quot;**从不**\&quot;。
    
      - **上次重播日志的时间**   显示 LogReplayer 上次将日志文件重播到选定数据库副本中的日期和时间戳。此字段仅与被动数据库副本相关。在主动数据库副本（已复制和独立）上，此字段显示\&quot;**从不**\&quot;。
    
      - **激活首选项编号**   显示激活首选项编号。它在活动管理器最佳副本选择过程中用到，并使用 RedistributeActiveDatabases.ps1 脚本在 DAG 中重新分布活动邮箱数据库，从而平衡 DAG。激活首选项的值为大于等于 1 的数字，1 表示最优先。此编号不能大于邮箱数据库的副本数。
    
      - **重播延隔时间(天)**   显示 Microsoft Exchange Information Store 服务在重播被 Microsoft Exchange Replication 服务复制到被动数据库副本的日志文件之前应等待的时间。将此参数的值设置为大于 0 会创建延隔数据库副本。此参数的默认值设置为 0 天，最大值为 14 天，最小值为 0 天。将此值设置为 0 会禁用重播延隔。

## 使用命令行管理程序配置邮箱数据库副本属性

本示例将一个邮箱数据库副本的激活首选项编号配置为 3。

    Set-MailboxDatabaseCopy -Identity DB3\EX3 -ActivationPreference 3

此示例将在 Server1 上驻留的数据库 DB1 的副本的重播延迟时间和截断延隔时间配置为 1 天，将激活首选项编号配置为 2。

    Set-MailboxDatabaseCopy -Identity DB1\Server1 -ReplayLagTime 1.0:0:0 -TruncationLagTime 1.0:0:0 -ActivationPreference 2

## 您如何知道这有效？

若要验证是否已成功配置邮箱数据库副本，请执行以下操作之一：

  - 在 EAC 中，导航至\&quot;服务器\&quot;\>\&quot;数据库\&quot;。选择相应数据库，然后在\&quot;详细信息\&quot;窗格中单击\&quot;查看详细信息\&quot;查看数据库备份属性。

  - 在命令行管理程序中运行以下命令来显示数据库备份的配置信息。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

## 详细信息

[Set-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298104\(v=exchg.150\))

[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-cn/library/dd298044\(v=exchg.150\))

[Get-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb124924\(v=exchg.150\))

