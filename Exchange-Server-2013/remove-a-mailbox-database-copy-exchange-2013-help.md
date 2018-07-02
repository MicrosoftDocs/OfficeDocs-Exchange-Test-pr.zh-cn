---
title: '删除邮箱数据库副本: Exchange 2013 Help'
TOCTitle: 删除邮箱数据库副本
ms:assetid: 99fecdde-b158-4dfc-9ca7-ff7c0ada7819
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298164(v=EXCHG.150)
ms:contentKeyID: 50491216
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除邮箱数据库副本

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-06_

这些是有关如何删除邮箱数据库的副本的过程。不能按这些过程操作，删除邮箱数据库的最后一个副本。有关删除邮箱数据库最后一个副本的详细步骤，请参阅[删除邮箱数据库](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)或 [Remove-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/aa997931\(v=exchg.150\))。

若要了解与邮箱数据库副本相关的其他管理任务，请查看[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;邮箱数据库副本\&quot;条目。

  - 邮箱数据库副本只能从处于正常状态的数据库可用性组 (DAG) 中删除。如果 DAG 不能正常运行（例如，由于仲裁丢失，DAG 的基础群集出现故障），将无法删除任何邮箱数据库副本。

  - 如果要删除数据库的最后一个被动副本，不得为指定邮箱数据库启用连续复制循环日志记录 (CRCL)。如果已启用 CRCL，则必须先禁用它。在删除邮箱数据库副本之后，才可以启用循环日志记录。在为未复制的邮箱数据库启用循环日志记录之后，使用的是 JET 循环日志记录，而不是 CRCL。如果不打算删除数据库的最后一个被动副本，可以继续启用 CRCL。

  - 删除数据库副本之后，必须手动从删除数据库副本的服务器上删除任何数据库和事务日志文件。

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

## 使用 EAC 删除邮箱数据库副本

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库\&quot;。

2.  选择要删除其副本的邮箱数据库。

3.  在\&quot;详细信息\&quot;窗格中，找到要删除的被动副本，然后单击\&quot;删除\&quot;。

4.  通过单击\&quot;是\&quot;在警告对话框中确认删除。

5.  单击\&quot;确定\&quot;确认删除检查完的任何消息。

6.  手动从删除数据库副本的服务器上删除任何数据库和事务日志文件。

## 使用命令行管理程序删除邮箱数据库副本

本示例从邮箱服务器 MBX1 删除邮箱数据库 DB1 的副本。

    Remove-MailboxDatabaseCopy -Identity DB1\MBX1 -Confirm:$False

## 您如何知道这有效？

要验证是否已成功删除邮箱数据库副本，请执行以下操作之一：

  - 在 EAC 中，依次转到\&quot;**服务器**\&quot;\>\&quot;**数据库**\&quot;。选择相应的数据库。此时，细节窗格中不再列出已删除的被动副本。

  - 在命令行管理程序中运行下列命令以验证副本删除操作。
    
        Get-MailboxDatabase <DatabaseName> | Format-List DatabaseCopies
    
    已删除的被动副本不再列出。

