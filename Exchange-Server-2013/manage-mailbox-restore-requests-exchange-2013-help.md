---
title: '管理邮箱还原请求: Exchange 2013 Help'
TOCTitle: 管理邮箱还原请求
ms:assetid: 8e668a52-c601-4d96-a51c-ab60267e1321
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ863437(v=EXCHG.150)
ms:contentKeyID: 50556639
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理邮箱还原请求

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

邮箱还原请求用于还原断开连接的邮箱。断开连接的邮箱是邮 Exchange 箱数据库中不与 Active Directory 用户帐户关联的邮箱。在禁用、删除邮箱或将邮箱移到其他数据库时，邮箱就会断开连接。有关详细信息，请参阅[断开连接的邮箱](disconnected-mailboxes-exchange-2013-help.md)。

断开的邮箱仍保留在邮箱数据库中，保留时间在邮箱数据库的已删除邮箱保留设置中指定。默认情况下，断开的邮箱将保留 30 天。在此保留期间，可将被删除的邮箱的内容还原（复制）到某个现有的邮箱。本主题描述如何使用命令行管理程序管理邮箱还原请求。

有关与断开连接的邮箱相关的其他管理任务，请参阅下列主题：

[禁用或删除邮箱](disable-or-delete-a-mailbox-exchange-2013-help.md)

[连接禁用的邮箱](connect-a-disabled-mailbox-exchange-2013-help.md)

[连接或还原已删除的邮箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

[还原软删除的邮箱](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

[永久删除邮箱](permanently-delete-a-mailbox-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“邮箱还原请求”条目。

  - 本主题中的此过程只能在命令行管理程序中执行。不能使用 EAC 查看邮箱还原请求。

  - 若要显示所有邮箱还原请求的 *Identity* 属性的值，请运行以下命令。
    
        Get-MailboxRestoreRequest | Format-Table Identity
    
    在执行本主题中的过程时，可以使用此标识值指定特定的邮箱还原请求。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用命令行管理程序查看还原请求属性

可以查看邮箱还原请求的属性，了解有关邮箱还原请求状态的基本信息。

若要显示所有邮箱还原请求的 *Identity* 属性的列表和值，请运行以下命令。

    Get-MailboxRestoreRequest | Format-Table Identity

可以使用该标识获取有关特定邮箱还原请求的信息。

此示例使用 *Identity* 参数返回还原请求 Pilar Pinilla \\MailboxRestore 的状态。

    Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore"

此示例返回 Pilar Pinilla 目标邮箱的第二个还原请求的所有信息。

    Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1" | Format-List

此示例返回从源数据库 MBD01 还原的还原请求的状态。

    Get-MailboxRestoreRequest -SourceDatabase MBD01

此示例返回当前正在进行的所有还原请求。

    Get-MailboxRestoreRequest -Status InProgress

其他有用的状态包括 `Queued`、`Completed`、`Suspended` 和 `Failed`。

此示例返回已挂起的所有还原请求。

    Get-MailboxRestoreRequest -Suspend $true

有关语法和参数的详细信息，请参阅 [Get-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829907\(v=exchg.150\))。

## Get-MailboxRestoreRequest 输出

默认情况下，**Get-MailboxRestoreRequest** cmdlet 返回请求的名称、要将数据还原到的目标邮箱以及请求的状态。下表列出在将 cmdlet 通过管道传输到 **Format-List** cmdlet 时返回的有用信息。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SourceDatabase</code></p></td>
<td><p>指定包含要还原的断开连接邮箱的数据库。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetMailbox</code></p></td>
<td><p>指定要将数据还原到其中的邮箱。</p></td>
</tr>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>指定请求的名称。</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>指定 Microsoft Exchange Mailbox Replication 服务 (MRS) 用于存储请求详细状态的数据库。</p></td>
</tr>
<tr class="odd">
<td><p><code>Status</code></p></td>
<td><p>指定请求的状态。</p></td>
</tr>
<tr class="even">
<td><p><code>Suspend</code></p></td>
<td><p>指定请求是否挂起。使用 <strong>New-MailboxRestoreRequest</strong> cmdlet 和 <em>Suspend</em> 参数创建邮箱还原时，可将邮箱还原挂起。如果邮箱还原操作失败，也可能会将邮箱还原挂起；管理员也可以使用 <strong>Suspend-MailboxRestoreRequest</strong> cmdlet 将邮箱还原挂起。</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>指定请求的标识。此标识是目标邮箱名称和请求名称的组合。</p></td>
</tr>
</tbody>
</table>


## 您如何知道这有效？

运行 **Get-MailboxRestoreRequest** cmdlet 可以验证是否可查看邮箱还原请求的属性。如果 cmdlet 返回错误，则验证使用的语法和标识是否正确。在有些情况下，该 cmdlet 可能是成功的，但不返回任何结果。例如，如果提交了一个邮箱还原请求，并运行了 `Get-MailboxRestoreRequest -Status InProgress`，但未返回任何结果，则表示当前没有任何还原请求正在运行。

## 使用命令行管理程序查看还原请求统计信息

可以查看邮箱还原请求的统计信息，其中提供了可用于故障排除的详细信息。

此示例返回还原请求 danp\\MailboxRestore1 的默认统计信息。默认情况下，返回的信息包括名称、邮箱、状态和完成百分比。

    Get-MailboxRestoreRequestStatistics -Identity danp\MailboxRestore1

本示例返回 Dan Park 的邮箱统计信息，并将报告导出到 .csv 文件中。

    Get-MailboxRestoreRequestStatistics -Identity "Dan Park\MailboxRestore" | Export-CSV \\SERVER01\RestoreRequest_Reports\DanPark_Restorestats.csv

此示例通过使用 *IncludeReport* 参数并将结果通过管道传输到 **Format-List** cmdlet，返回有关 Pilar Pinilla 邮箱的还原请求的其他信息。

    Get-MailboxRestoreRequestStatistics -Identity "Pilar Pinilla\MailboxRestore" -IncludeReport | Format-List 

此示例通过使用 *IncludeReport* 参数返回状态为 `Failed` 的所有还原请求的其他信息，然后将这些信息保存到文件 AllRestoreReports.txt（位于正在运行此命令的位置）。

    Get-MailboxRestoreRequest -Status Failed | Get-MailboxRestoreRequestStatistics -IncludeReport | Format-List > AllRestoreReports.txt

有关语法和参数的详细信息，请参阅 [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/zh-cn/library/ff829912\(v=exchg.150\)) 和 [Get-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829907\(v=exchg.150\))。

## Get-MailboxRestoreRequestStatistics 输出

默认情况下，[Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/zh-cn/library/ff829912\(v=exchg.150\)) cmdlet 返回请求的名称、请求的状态、目标邮箱的别名以及完成的百分比。下表列出在将 cmdlet 通过管道传输到 **Format-List** cmdlet 时返回的其他有用信息。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>指定请求的名称。</p></td>
</tr>
<tr class="even">
<td><p><code>Status</code></p></td>
<td><p>指定请求的状态。</p></td>
</tr>
<tr class="odd">
<td><p><code>StatusDetail</code></p></td>
<td><p>指定有关请求状态的更多详细信息。例如，如果 <code>Status</code> 值返回 <code>InProgress</code>，则 <code>StatusDetail</code> 值会返回 <code>InProgress</code> 状态的特定阶段，如 <code>CreatingFolderHierarchy</code> 和 <code>CopyingMessages</code>。</p></td>
</tr>
<tr class="even">
<td><p><code>SyncStage</code></p></td>
<td><p>指定请求在还原过程中的进展情况。</p></td>
</tr>
<tr class="odd">
<td><p><code>Suspend</code></p></td>
<td><p>指定还原请求是否挂起。此值在以下情况中为 <code>true</code>：</p>
<ul>
<li><p>MRS 由于失败已停止或正在停止请求。</p></li>
<li><p>管理员挂起了请求。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SourceExchangeGuid</code></p></td>
<td><p>指定要从中还原数据的源邮箱的 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><code>SourceRootFolder</code></p></td>
<td><p>指定要从中还原数据的源邮箱层次结构中的根文件夹名称。如果此值为空，则数据会从“信息存储顶部”文件夹还原。</p></td>
</tr>
<tr class="even">
<td><p><code>SourceDatabase</code></p></td>
<td><p>指定源邮箱所处的数据库的名称。</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxRestoreFlags</code></p></td>
<td><p>指定要还原的邮箱是 <code>Disabled</code> 还是 <code>Soft-Deleted</code>。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetAlias</code></p></td>
<td><p>指定目标邮箱的别名。</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetIsArchive</code></p></td>
<td><p>指定邮箱是否要还原到存档中。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetExchangeGuid</code></p></td>
<td><p>指定目标邮箱的 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetRootFolder</code></p></td>
<td><p>指定要将数据还原到的目标邮箱层次结构中的根文件夹名称。如果此值为空，则数据会还原到“信息存储顶部”文件夹中。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetDatabase</code></p></td>
<td><p>指定目标邮箱所处的数据库的名称。</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetMailboxIdentity</code></p></td>
<td><p>指定目标邮箱的标识。</p></td>
</tr>
<tr class="even">
<td><p><code>IncludeFolders</code></p></td>
<td><p>指定在还原过程中要包括的文件夹列表。如果此值为空，则创建请求时未指定任何文件夹，并且所有文件夹都将还原到邮箱中（除非使用 <em>ExcludeFolders</em> 参数排除特定文件夹）。</p></td>
</tr>
<tr class="odd">
<td><p><code>ExcludeFolders</code></p></td>
<td><p>指定在还原过程中要排除的文件夹列表。如果此值为空，则创建请求时未指定任何文件夹，并且所有文件夹都将还原到邮箱中（除非使用 <em>IncludeFolders</em> 参数包括特定文件夹）。</p></td>
</tr>
<tr class="even">
<td><p><code>ExcludeDumpster</code></p></td>
<td><p>指定创建请求时是否排除了“可恢复的项目”文件夹。</p></td>
</tr>
<tr class="odd">
<td><p><code>ConflictResolutionOption</code></p></td>
<td><p>指定当目标和源文件夹中存在匹配邮件时，MRS 要执行的操作。</p></td>
</tr>
<tr class="even">
<td><p><code>AssociatedMessagesCopyOption</code></p></td>
<td><p>指定处理请求时是否复制关联邮件。关联邮件指包含隐藏数据（其中包含有关规则、视图和窗体的信息）的特殊邮件。</p></td>
</tr>
<tr class="odd">
<td><p><code>BadItemLimit</code></p></td>
<td><p>指定在请求遇到损坏邮件时 MRS 将跳过的错误项目数。</p></td>
</tr>
<tr class="even">
<td><p><code>BadItemsEncountered</code></p></td>
<td><p>指定命令遇到的已损坏邮件数。如果 <em>BadItemsEncountered</em> 值大于 <em>BadItemLimit</em> 值，则请求失败。</p></td>
</tr>
<tr class="odd">
<td><p><code>QueuedTimeStamp</code></p></td>
<td><p>指定向 MRS 发起请求的日期和时间。</p></td>
</tr>
<tr class="even">
<td><p><code>StartTimeStamp</code></p></td>
<td><p>指定 MRS 开始处理还原请求的日期和时间。</p></td>
</tr>
<tr class="odd">
<td><p><code>LastUpdateTimeStamp</code></p></td>
<td><p>指定上次对请求进行更改的日期和时间。更改可能由管理员或 MRS 进行。</p></td>
</tr>
<tr class="even">
<td><p><code>SuspendTimeStamp</code></p></td>
<td><p>指定挂起请求的日期和时间。</p></td>
</tr>
<tr class="odd">
<td><p><code>OverallDuration</code></p></td>
<td><p>指定完成请求所花费的时间量。如果请求的状态为 <code>Failed</code>，则此值指定发起请求和请求失败之间的时间量。如果请求尚未完成，则此值指定发起请求与运行 <strong>Get-MailboxRestoreRequestStatistics</strong> cmdlet 之间的时间量。</p></td>
</tr>
<tr class="even">
<td><p><code>TotalSuspendedDuration</code></p></td>
<td><p>指定请求处于 <code>Suspended</code> 状态的时间量。</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalFailedDuration</code></p></td>
<td><p>指定请求处于 <code>Failed</code> 状态的时间量。</p></td>
</tr>
<tr class="even">
<td><p><code>TotalQueuedDuration</code></p></td>
<td><p>指定请求处于 <code>Queued</code> 状态的时间量。</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalInProgressDuration</code></p></td>
<td><p>指定请求处于 <code>In Progress</code> 状态的时间量。</p></td>
</tr>
<tr class="even">
<td><p><code>TotalStalledDueToHADuration</code></p></td>
<td><p>指定由于高可用性而使请求停止的时间量。</p></td>
</tr>
<tr class="odd">
<td><p><code>MRSServerName</code></p></td>
<td><p>指定处理请求的客户端访问服务器的名称。</p></td>
</tr>
<tr class="even">
<td><p><code>EstimatedTransferSize</code></p></td>
<td><p>指定已还原的文件总大小，或者在请求处于 <code>In Progress</code> 状态时 MRS 期望还原的文件大小。</p></td>
</tr>
<tr class="odd">
<td><p><code>EstimatedTransferItemCount</code></p></td>
<td><p>指定已还原的项目数或在请求处于 <code>In Progress</code> 状态时 MRS 期望还原的项目数。</p></td>
</tr>
<tr class="even">
<td><p><code>BytesTransferredPerMinute</code></p></td>
<td><p>指定每分钟已传输的平均字节数。</p></td>
</tr>
<tr class="odd">
<td><p><code>ItemsTransferred</code></p></td>
<td><p>指定已传输的项目数。</p></td>
</tr>
<tr class="even">
<td><p><code>PercentComplete</code></p></td>
<td><p>指定已完成的请求百分比。</p></td>
</tr>
<tr class="odd">
<td><p><code>CompletedRequestAgeLimit</code></p></td>
<td><p>指定在完成的还原请求在被删除之前的保留时间。默认为 30 天。</p></td>
</tr>
<tr class="even">
<td><p><code>PositionInQueue</code></p></td>
<td><p>如果尚未开始请求，则此值指定请求在队列中的位置。</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureCode</code></p></td>
<td><p>如果失败，则此值指定失败代码。</p></td>
</tr>
<tr class="even">
<td><p><code>FailureType</code></p></td>
<td><p>如果失败，则此值指定失败类型。</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureSide</code></p></td>
<td><p>如果失败，则此值指定失败是在目标邮箱还是源邮箱上发生。</p></td>
</tr>
<tr class="even">
<td><p><code>Message</code></p></td>
<td><p>如果失败，则此值指定失败消息。此值还可以指定挂起注释。</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureTimestamp</code></p></td>
<td><p>如果请求失败，则此值指定请求失败的日期和时间。</p></td>
</tr>
<tr class="even">
<td><p><code>FailureContext</code></p></td>
<td><p>如果请求失败，则此值指定有关在失败时执行的操作的信息。</p></td>
</tr>
<tr class="odd">
<td><p><code>ValidationMessage</code></p></td>
<td><p>如果请求无效，则此值指定原因。</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>指定 MRS 用于存储请求的详细状态的数据库。</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>指定请求的标识。</p></td>
</tr>
<tr class="even">
<td><p><code>Report</code></p></td>
<td><p>如果使用了 <em>IncludeReport</em> 参数，则此值指定可以用于解决请求问题的信息。</p></td>
</tr>
</tbody>
</table>


## 您如何知道这有效？

运行 **Get-MailboxRestoreRequestStatistics** cmdlet 可以验证是否可查看邮箱还原请求的统计信息。如果 cmdlet 返回错误，则验证使用的还原请求标识是否正确。

## 使用命令行管理程序更改还原请求属性

如果邮箱还原请求失败，则可使用 **Set-MailboxRestoreRequest** cmdlet 更改请求属性以深度从失败中恢复。

此示例指定对 Debra Garcia 邮箱的还原请求 MailboxRestore1 跳过 10 个损坏的邮箱项目。

    Set-MailboxRestoreRequest -Identity "Debra Garcia\MailboxRestore1" -BadItemLimit 10

此示例指定对 Florence Flipo 邮箱的还原请求 MailboxRestore1 跳过 100 个损坏的项目。由于 *BadItemLimit* 值大于 50，因此必须指定 *AcceptLargeDataLoss* 参数。

    Set-MailboxRestoreRequest -Identity "Florence Flipo\MailboxRestore1" -BadItemLimit 100 -AcceptLargeDataLoss

有关语法和参数的详细信息，请参阅 [Set-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829909\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功更改了还原请求的属性，请运行 **Get-MailboxRestoreRequestStatistics** cmdlet 以显示经过修订的还原请求属性。如果成功创建了还原请求，则 *Status* 属性的值将为 `Queued`、`InProgress` 或 `Completed`。还原请求完成后，软删除的邮箱的内容将出现在目标邮箱中。

有关语法和参数的详细信息，请参阅 [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/zh-cn/library/ff829912\(v=exchg.150\))。

## 使用命令行管理程序挂起还原请求

可以在创建某个还原请求之后随时挂起该请求，但是要在该请求到达 `Completed` 状态之前进行。有关使用 [Resume-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829908\(v=exchg.150\)) cmdlet 恢复还原请求的命令语法，请参阅本主题中稍后的使用命令行管理程序恢复还原请求。

此示例挂起对 Pilar Pinilla 邮箱的还原请求 MailboxRestore1。

    Suspend-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

此示例挂起所有正在处理的还原请求，具体方法是：先检索状态为 `InProgress` 的所有请求，继而通过管道将输出传递给 **Suspend-MailboxRestoreRequest** cmdlet，并给出挂起注释“Resume after FY13Q2 Maintenance”。

    Get-MailboxRestoreRequest -Status InProgress | Suspend-MailboxRestoreRequest -SuspendComment "Resume after FY13Q2 Maintenance"

有关语法和参数的详细信息，请参阅 [Suspend-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829906\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功挂起了邮箱还原请求，请运行以下命令。

    Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status

如果 *Suspend* 属性的值等于 `True`，则表示已成功挂起还原请求。此外，*Status* 属性的值 `Suspended` 表示还原请求已挂起。

## 使用命令行管理程序恢复还原请求

使用 **Resume-MailboxRestoreRequest** cmdlet 可以恢复已失败或已挂起的还原请求。

此示例恢复还原请求 Pilar Pinilla\\MailboxRestore1。

    Resume-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

此示例恢复状态为“失败”的所有还原请求。

    Get-MailboxRestoreRequest -Status Failed | Resume-MailboxRestoreRequest

有关语法和参数的详细信息，请参阅 [Resume-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829908\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已恢复还原请求，请运行以下命令。

    Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status

如果 *Suspend* 属性的值等于 `False`，则表示已成功恢复还原请求。此外，*Status* 属性的值 `InProgress` 表示还原请求已恢复。

## 使用命令行管理程序删除还原请求

可以使用 **Remove-MailboxRestoreRequest** cmdlet 删除邮箱还原请求。如果在开始将邮箱数据复制到目标邮箱之后删除还原请求，则被复制的邮箱数据会保留在目标邮箱中。

> [!NOTE]
> 如前所述，默认情况下，完成的还原请求会保留 30 天，然后被自动删除。


此示例删除还原请求 Pilar Pinilla\\MailboxRestore1。

    Remove-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

本示例将删除状态为“已完成”的所有还原请求。

    Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest

本示例通过使用 *RequestGuid* 参数取消存储在 MBXDB01 上的某请求的还原请求。需要 *RequestGuid* 和 *RequestQueue* 参数的参数集仅用于 Microsoft 复制服务调试目的。只应在 Microsoft 客户服务和支持的指导下使用此参数集。

    Remove-MailboxRestoreRequest -RequestQueue MBXDB01 -RequestGuid 25e0eaf2-6cc2-4353-b83e-5cb7b72d441f

有关语法和参数的详细信息，请参阅 [Remove-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829910\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功删除了邮箱还原请求，请运行以下命令。

    Get-MailboxRestoreRequest -Identity <identity of removed restore request>

该命令将返回一个错误，指出还原请求不存在。

也可以使用 **Get-MailboxRestoreRequest** cmdlet。如果成功删除了还原请求，则不会将其包括在结果中。

