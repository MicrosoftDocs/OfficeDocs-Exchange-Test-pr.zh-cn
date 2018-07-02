---
title: '激活滞后的邮箱数据库副本: Exchange 2013 Help'
TOCTitle: 激活滞后的邮箱数据库副本
ms:assetid: 493d9c40-644d-49d6-9291-949acbcfdcb6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd979786(v=EXCHG.150)
ms:contentKeyID: 50490447
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 激活滞后的邮箱数据库副本

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-01-28_

滞后的邮箱数据库副本是一种重播延迟时间值配置为大于 0 的邮箱数据库副本。如果要数据库重播所有日志文件，并使数据库副本保持最新，那么激活和恢复滞后的邮箱数据库副本将是一个很简单的过程。如果要重播截止到特定时间点的日志文件，操作将更加困难，因为您必须手动处理日志文件并运行 Eseutil。

若要了解与滞后邮箱数据库副本相关的其他信息，请查看[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>激活滞后的邮箱数据库副本所需的时间直接取决于重播日志文件的多少和硬件重播日志文件的速度。应看到的日志重播速度至少为每个数据库每秒钟两个日志文件。</td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：一分钟，加上复制滞后副本、替换必需的日志文件和提取数据或装入数据库客户端活动所需的时间。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;邮箱数据库副本\&quot;条目。

  - 要激活邮箱数据库副本的重播延迟时间必须配置为大于 0。

  - 要激活邮箱数据库副本所拥有的全部日志文件的时间点必须达到希望恢复到的时间点。确定要恢复到的时间点时，请记住数据库事务可以跨多个日志文件。

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

## 使用命令行管理程序将滞后的邮箱数据库副本激活到特定时间点

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不能使用 EAC 将滞后邮箱数据库副本激活到特定时间点。而是使用命令行管理程序和命令行执行一系列步骤。</td>
</tr>
</tbody>
</table>


1.  此示例将挂起通过使用 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd351074\(v=exchg.150\)) cmdlet 激活的滞后副本的复制操作。
    
        Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false

2.  或者（若要保留滞后副本），为数据库副本及其日志文件创建一个副本。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此时，继续在现有卷上执行此过程会导致副本在写入性能方面受到影响。如果不想发生这样的情况，可以将数据库和日志文件复制到另一个卷以执行恢复。</td>
    </tr>
    </tbody>
    </table>


3.  确定必须将哪些日志文件重播到数据库中才能符合此恢复过程的时间要求（根据日志文件的日期和时间，如 Windows 资源管理器中所示）。在此之后创建的所有日志都应移至另一目录，直到恢复过程结束，并且不再需要这些日志。

4.  删除数据库的检查点 (.chk) 文件。

5.  此示例使用 Eseutil 执行恢复操作。
    
        Eseutil.exe /r eXX /a
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在前面的示例中，<em>XX</em> 是数据库的日志生成前缀（例如，E00、E01、E02 等等）。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此步骤可能会花费相当长的时间，这取决于多种因素，如重播延迟时间的长度、该期间内生成的日志文件数量以及硬件将这些日志重播到进行恢复的数据库的速度。</td>
    </tr>
    </tbody>
    </table>


6.  日志重播完成后，数据库将处于干净关闭状态，可以对其进行复制并用于恢复目的。

7.  恢复过程完成后，此示例将继续进行用作恢复过程一部分的数据库复制操作。
    
        Resume-MailboxDatabaseCopy DB1\EX3

有关语法和参数的详细信息，请参阅 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd351074\(v=exchg.150\)) 和 [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335220\(v=exchg.150\))。

## 通过重播所有未提交的日志文件，使用命令行管理程序激活滞后邮箱数据库副本

1.  或者（若要保留滞后副本），为数据库副本及其日志文件创建一个副本。
    
    1.  此示例将挂起通过使用 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd351074\(v=exchg.150\)) cmdlet 激活的滞后副本的复制操作。
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  或者（若要保留滞后副本），为数据库副本及其日志文件创建一个副本。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>此时，继续在现有卷上执行此过程会导致副本在写入性能方面受到影响。如果不想发生这样的情况，可以将数据库和日志文件复制到另一个卷以执行恢复。</td>
        </tr>
        </tbody>
        </table>


2.  此示例将通过使用 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/zh-cn/library/dd298068\(v=exchg.150\)) cmdlet 以及 *SkipLagChecks* 参数激活滞后的邮箱数据库副本。
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -SkipLagChecks

## 使用命令行管理程序并通过 SafetyNet 恢复激活滞后的邮箱数据库副本

1.  或者（若要保留滞后副本），对包含数据库副本及其日志文件的卷生成基于文件系统（非 Exchange 感知）的卷影复制服务 (VSS) 快照。
    
    1.  此示例将挂起通过使用 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd351074\(v=exchg.150\)) cmdlet 激活的滞后副本的复制操作。
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  或者（若要保留滞后副本），为数据库副本及其日志文件创建一个副本。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>此时，继续在现有卷上执行此过程会导致副本在写入性能方面受到影响。如果不想发生这样的情况，可以将数据库和日志文件复制到另一个卷以执行恢复。</td>
        </tr>
        </tbody>
        </table>


2.  通过查找 ESEUTIL 数据库头输出中的\&quot;所需的日志:\&quot;值来确定滞后数据库副本所需的日志
    
        Eseutil /mh <DBPath> | findstr /c:"Log Required"
    
    记下圆括号中的十六进制数字。第一个数字是所需的最低生成（也称为 LowGeneration），第二个数字是所需的最高生成（也称为 HighGeneration）。将所有生成序列大于 HighGeneration 的日志生成文件移到到其他位置，以便它们不会重播到数据库中。

3.  在托管数据库主动副本的服务器中，为从主动副本激活的滞后副本删除日志文件，或停止 Microsoft Exchange 复制服务。

4.  执行数据库切换并激活滞后副本。此示例使用 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/zh-cn/library/dd298068\(v=exchg.150\)) cmdlet 以及几个参数激活数据库。
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -MountDialOverride BestEffort -SkipActiveCopyChecks -SkipClientExperienceChecks -SkipHealthChecks -SkipLagChecks

5.  此时，数据库将自动装入，并从 SafetyNet 请求重新交付丢失的邮件。

## 您如何知道这有效？

要验证是否已成功激活滞后的邮箱数据库副本，请执行以下操作之一：

  - 在 EAC 中，导航至\&quot;服务器\&quot;\>\&quot;数据库\&quot;。选择相应数据库，然后在\&quot;详细信息\&quot;窗格中单击\&quot;查看详细信息\&quot;查看数据库备份属性。

  - 在命令行管理程序中，运行以下命令来显示数据库备份的状态信息。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

