---
title: '创建恢复数据库: Exchange 2013 Help'
TOCTitle: 创建恢复数据库
ms:assetid: 34d87491-b7b7-44a9-8d69-e1a9c1fe5852
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee332321(v=EXCHG.150)
ms:contentKeyID: 50490296
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建恢复数据库

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-01-21_

您可以使用 Shell 创建恢复数据库，这类特殊的邮箱数据库作为恢复操作的一部分，用于装入已还原的数据库并从中提取数据。在创建恢复数据库之后，可以将恢复或还原的邮箱数据库移动到恢复数据库中，然后使用 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829875\(v=exchg.150\)) cmdlet 从恢复的数据库提取数据。在提取之后，即可将数据导出到文件夹或合并到现有邮箱中。使用恢复数据库，可以通过数据库的备份或副本来恢复数据，而无须干扰用户对当前数据的访问。

若要了解与恢复数据库相关的其他管理任务，请查看[恢复数据库](recovery-databases-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;邮箱恢复\&quot;条目。

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


## 使用命令行管理程序创建恢复数据库

本示例在邮箱服务器 MBX2 上创建恢复数据库 RDB1。

    New-MailboxDatabase -Recovery -Name RDB1 -Server MBX2

本示例使用数据库文件和日志文件夹的自定义路径在邮箱服务器 MBX1 上创建恢复数据库 RDB2。

    New-MailboxDatabase -Recovery -Name RDB2 -Server MBX1 -EdbFilePath "C:\Recovery\RDB2\RDB2.EDB" -LogFolderPath "C:\Recovery\RDB2"

有关语法和参数的详细信息，请参阅 [New-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/aa997976\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功创建了恢复数据库，请执行以下操作：

  - 在命令行管理程序中，运行下列命令来显示恢复数据库的配置信息。
    
        Get-MailboxDatabase <RecoveryDatabaseName> | Format-List

## 其他任务

在创建恢复数据库之后，还可能需要使用恢复数据库还原数据。有关详细步骤，请参阅[使用恢复数据库还原数据](restore-data-using-a-recovery-database-exchange-2013-help.md)。

