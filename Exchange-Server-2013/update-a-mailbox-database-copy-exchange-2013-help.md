---
title: '更新邮箱数据库副本: Exchange 2013 Help'
TOCTitle: 更新邮箱数据库副本
ms:assetid: bead3cc5-7d50-446f-95b7-e432bcb7968e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351100(v=EXCHG.150)
ms:contentKeyID: 50491563
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更新邮箱数据库副本

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-11-02_

更新（亦称为\&quot;*种子设定*\&quot;）是将邮箱数据库副本添加到数据库可用性组 (DAG) 中另一邮箱服务器的过程。新添加的副本将成为被动副本的基线数据库，其中将重播从主动副本复制的日志文件。在下列情况下必须设定种子：

  - 新建数据库的被动副本时。对于新的邮箱数据库副本，可以推迟种子设定；但最终每个被动数据库副本都必须设定种子，才能用作冗余数据库副本。

  - 在发生由于被动数据库副本出现变化且不可恢复而导致数据丢失的故障后。

  - 当系统检测到不能重播到数据库被动副本的损坏的日志文件时。

  - 任一数据库副本进行脱机碎片整理后。

  - 在数据库的日志生成序列重置回 1 后。

可以使用以下方法执行种子设定：

  - **自动种子设定**   自动种子设定在数据库创建期间执行，用于在目标邮箱服务器上生成活动数据库的被动副本。

  - **使用 Update-MailboxDatabaseCopy cmdlet 设定种子**   可以随时在命令行管理程序中使用 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 将数据库副本设定为种子。

  - **使用\&quot;更新邮箱数据库副本\&quot;向导设定种子**   可以在 EAC 中随时使用更新邮箱数据库副本向导将数据库副本设定为种子。

  - **手动复制脱机数据库** 可以卸除数据库的主动副本，并将数据库文件复制到同一 DAG 中另一邮箱服务器上的同一位置。使用此方法时，会遇到服务中断，因为此过程需要卸除数据库。

更新数据库副本可能需要很长时间才能完成，尤其当要复制的数据库很大或者网络延迟严重或网络带宽很低时。种子设定过程启动后，请勿在此过程结束前关闭 EAC 或命令行管理程序。否则，种子设定操作会终止。

可将主动副本或最新被动副本用作种子设定的源，为数据库副本设定种子。从被动副本设定种子时，请注意，在以下几种情况下，若出现网络通信错误，则种子设定操作会终止：

  - 种子设定源副本的状态更改为\&quot;已失败\&quot;或 FailedAndSuspended 时。

  - 数据库故障转移到其他副本时。

可以同时为多个数据库副本设定种子。不过，若同时为多个副本设定种子，只能对数据库文件设定种子，并省略内容索引目录。为此，可以结合使用 *DatabaseOnly* 参数和 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果在从同一源为多个目标设定种子时不使用 <em>DatabaseOnly</em> 参数，此任务将失败，出现 SeedInProgressException 错误 FE1C6491。</td>
</tr>
</tbody>
</table>


若要了解与邮箱数据库副本相关的其他管理任务，请查看[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 该任务的估计完成时间：2 分钟，外加数据库副本的种子设定时间，时间长短取决于各种因素，如数据库大小、速度、可用带宽和网络延迟以及存储速度。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;邮箱数据库副本\&quot;条目。

  - 必须暂停邮箱数据库副本。有关详细步骤，请参阅[挂起或恢复邮箱数据库副本](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md)。

  - 托管要更新的被动数据库副本的服务器上必须运行远程注册表服务。

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

## 使用 EAC 更新邮箱数据库副本

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库\&quot;。

2.  选择您要更新其被动副本的邮箱数据库。

3.  在细节窗格的\&quot;**数据库副本**\&quot;下，单击要设定种子的被动数据库副本下的\&quot;**暂停**\&quot;。提供任意可选注释，然后单击\&quot;**保存**\&quot;。

4.  在\&quot;详细信息\&quot;窗格的\&quot;数据库副本\&quot;下，单击您要设定种子的被动数据库副本下的\&quot;更新\&quot;。

5.  
    
    默认情况下，数据库的主动副本用作种子设定的源数据库。如果希望使用数据库的被动副本设定种子，请单击\&quot;**浏览…**\&quot;，选择包含要用作源的被动数据库副本的服务器。

6.  单击\&quot;保存\&quot;更新被动数据库副本。

## 使用命令行管理程序更新邮箱数据库副本

本示例显示如何对 MBX1 上的数据库 DB1 的副本设定种子。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1

本示例显示如何使用 MBX2 作为种子的源邮箱服务器对 MBX1 上的数据库 DB1 的副本设定种子。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2

本示例显示如何对 MBX1 上的数据库 DB1 的副本设定种子，而不对内容索引编录设定种子。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -DatabaseOnly

本示例显示如何对 MBX1 上的数据库 DB1 的副本的内容索引编录设定种子，而不对数据库文件设定种子。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly

## 手动复制脱机数据库

1.  如果为数据库启用循环日志记录，则在继续之前必须先禁用它。通过使用 [Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\)) cmdlet 可以禁用邮箱数据库的循环日志记录，如本例中所示。
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $false

2.  卸除数据库。可以使用 [Dismount-Database](https://technet.microsoft.com/zh-cn/library/bb124936\(v=exchg.150\)) cmdlet，如此示例中所示。
    
        Dismount-Database DB1 -Confirm $false

3.  手动将数据库文件（数据库文件和所有日志文件）复制到第二个位置，例如外部磁盘驱动器或网络共享。

4.  装载数据库。可以使用 [Mount-Database](https://technet.microsoft.com/zh-cn/library/aa998871\(v=exchg.150\)) cmdlet，如此示例中所示。
    
        Mount-Database DB1

5.  在托管副本的服务器上，将数据库文件从外部驱动器或网络共享复制到与主动数据库副本相同的路径。例如，如果主动数据库副本路径为 D:\\DB1\\DB1.edb，日志文件路径为 D:\\DB1，则可以将数据库文件复制到将托管副本的服务器上的 D:\\DB1。

6.  通过使用 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298105\(v=exchg.150\)) cmdlet 和 *SeedingPostponed* 参数，添加邮箱数据库副本，如此示例中所示。
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -SeedingPostponed

7.  如果为数据库启用循环日志记录，则使用 [Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\)) cmdlet 再次启用它，如此示例中所示。
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $true

## 您如何知道这有效？

要验证是否已成功设定邮箱数据库副本种子，请执行以下操作之一：

  - 在 EAC 中，依次转到\&quot;**服务器**\&quot;\>\&quot;**数据库**\&quot;。选择已设定种子的数据库。此时，细节窗格中会显示数据库副本的状态及其内容索引，以及当前的复制队列长度。

  - 在命令行管理程序中，运行以下命令验证是否已成功为邮箱数据库副本设定种子并且种子处于健康状态。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    状态和内容索引状态应该为健康。

