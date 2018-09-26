---
title: '可用于邮件记录管理的性能计数器: Exchange 2013 Help'
TOCTitle: 可用于邮件记录管理的性能计数器
ms:assetid: b59def6f-4249-4e0c-8057-8ae6eb7c5676
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb310790(v=EXCHG.150)
ms:contentKeyID: 51408265
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 可用于邮件记录管理的性能计数器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

本主题中的性能计数器监视托管文件夹助理它实现 Microsoft Exchange Server 2010的邮件记录管理 (MRM)。因为运行托管文件夹助理是一个非常耗费资源的过程，您应该仅在您的服务器可以承受额外增加的负载时运行它。托管文件夹助理正在运行时，还应监视服务器的性能。除了本主题中列出的性能计数器，您可以监视监视磁盘性能和 CPU 使用率等项目的其他性能计数器。

有关监视运行 MRM 的计算机的详细信息，请参阅[监视邮件记录管理](monitoring-https://technet.microsoft.com/zh-cn/library/dd335093(v=exchg.150))。

## MRM 的性能计数器

下表介绍了 MRM 的性能计数器。

### 性能计数器、性能对象和说明

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>性能计数器</th>
<th>性能对象</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Average Mailbox Processing Time In Seconds</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>计算基于时间的助理对邮箱的平均处理时间。</p></td>
</tr>
<tr class="even">
<td><p>Mailboxes Processed</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>计算自从服务启动后基于时间的助理已处理的邮箱数。</p></td>
</tr>
<tr class="odd">
<td><p>Mailboxes processed/sec</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>确定基于时间的助理每秒处理邮箱的速率。</p></td>
</tr>
<tr class="even">
<td><p>Items Deleted but Recoverable</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>统计的最新计划的时间间隔启动以来被托管文件夹助理程序删除的项的数目。（项目是通过恢复项文件夹仍可恢复。此数量包括在计划时间间隔并指定处理任何邮箱中的项目期间处理的邮箱中项目。此计数器将重置为零开头的每个计划时间间隔。</p></td>
</tr>
<tr class="odd">
<td><p>Items Journaled</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>计算项的数目的最新计划的时间间隔启动以来对托管文件夹助理。此数目包括任何用于处理指定的邮箱中的项与当前工作周期期间处理邮箱中项目。此计数器将重置为零起点的每个工作周期。</p></td>
</tr>
<tr class="even">
<td><p>Items Marked as Past Retention Date</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>对标记的项超过保留日期由托管文件夹助理的最新计划的时间间隔启动以来数进行计数。此数量包括在计划时间间隔并指定处理任何邮箱中的项目期间处理邮箱中项目。此计数器将重置为零开头的每个计划时间间隔。</p></td>
</tr>
<tr class="odd">
<td><p>Items Moved</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>统计的最新计划的时间间隔启动以来通过托管文件夹助理移动的项的数目。此数量包括在计划时间间隔并指定处理任何邮箱中的项目期间处理的邮箱中项目。此计数器将重置为零开头的每个计划时间间隔。</p></td>
</tr>
<tr class="even">
<td><p>Items Permanently Deleted</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>计算由托管文件夹助理的最新计划的时间间隔开始后永久删除的项的数目。此数量包括在计划时间间隔并指定处理任何邮箱中的项目期间处理的邮箱中项目。此计数器将重置为零开头的每个计划时间间隔。</p></td>
</tr>
<tr class="odd">
<td><p>Items Subject to Retention Policy</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>统计的最新计划的时间间隔启动以来受到由托管文件夹助理的保留策略的项目数。此数量包括在计划时间间隔并指定处理任何邮箱中的项目期间处理的邮箱中项目。此计数器将重置为零开头的每个计划时间间隔。此计数器是下列四个到期相关计数器的总和 ︰</p>
<ul>
<li><p>Items Journaled</p></li>
<li><p>Items Marked as Past Retention Date</p></li>
<li><p>Items Moved</p></li>
<li><p>Items Permanently Deleted</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsExpired - 受保留策略限制的项目大小（单位为字节）</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示托管文件夹助理（SoftDelete、HardDelete、MoveToArchive）使其过期的项目的总大小。</p>
<p>包括以下项目：</p>
<ul>
<li><p>通过托管文件夹邮箱策略被删除或移动到托管自定义文件夹的邮件</p></li>
<li><p>通过用户的保留策略被删除或移动到存档的邮件</p></li>
<li><p>由转储程序策略终止期限的邮件</p></li>
<li><p>通过系统清理标记清理的邮件</p></li>
</ul>
<p>在托管文件夹助理工作周期的每个工作周期检查点，将此计数器重置为零。</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsSoftDeleted - 已删除但可恢复的项目大小（单位为字节）</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示托管文件夹助理软删除的项目的总大小。</p>
<p>包括以下项目：</p>
<ul>
<li><p>通过托管文件夹邮箱策略软删除的邮件</p></li>
<li><p>通过保留策略软删除的邮件</p></li>
</ul>
<p>在托管文件夹助理工作周期的每个工作周期检查点，将此计数器重置为零。</p></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsPermanentlyDeleted - 永久删除的项目大小（单位为字节）</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示托管文件夹助理软删除的项目的总大小。</p>
<p>包括以下项目：</p>
<ul>
<li><p>通过托管文件夹邮箱策略硬删除的邮件</p></li>
<li><p>通过保留策略硬删除的邮件</p></li>
<li><p>通过可恢复项目策略硬删除的邮件</p></li>
</ul>
<p>在托管文件夹助理工作周期的每个工作周期检查点，将此计数器重置为零。</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsMoved - 由于存档策略标记导致移动的项目大小（单位为字节）</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示托管文件夹助理移动至文件夹或存档的项目的总大小。</p>
<p>包括以下项目：</p>
<ul>
<li><p>通过托管文件夹邮箱策略移动至托管自定义文件夹的邮件</p></li>
<li><p>通过保留策略移动至个人存档的邮件</p></li>
</ul>
<p>在托管文件夹助理工作周期的每个工作周期检查点，将此计数器重置为零。</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsWithPersonalTag - 带有个人标记（过期或存档）的项目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示用户用个人标记对项目标记的次数。</p>
<p>这包括删除和存档标记。</p>
<p>例如：</p>
<ul>
<li><p>项目使用个人标记进行标记。</p></li>
<li><p>使用另一个个人标记对带有个人标记的项目进行重新标记。</p></li>
</ul>
<p>如果某个文件夹使用个人标记进行标记，则计数器按该文件夹中的项目总数递增。</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsWithDefaultTag - 带有默认标记（过期或存档）的项目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示基于用户操作（例如，当用户选择带有个人标记的邮件并选择&amp;quot;使用文件夹策略&amp;quot;时）分配了默认策略标记 (DPT) 的项目数。</p>
<p>如果向新用户分配了一个带有 DPT 的保留策略，则计数器会按根据该保留策略分配 DPT 的项目数进行递增。</p>

> [!NOTE]  
> 如果用户具有带有 DPT 的保留策略，则通过传输到达的新邮件会获取默认标记，而此计数器不会对此进行跟踪。

</td>
</tr>
<tr class="even">
<td><p>TotalItemsWithSystemCleanupTag - 带有系统清理标记的项目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示与系统清理标签标记的项的数目。这包括对用户不可见的邮箱元数据项目。</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsExpiredByDefaultExpiryTag - 由于默认过期标记导致过期的项目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示由于保留策略中的任何非个人（默认或系统）标记而由托管文件夹助理终止期限（软删除或硬删除）的项目数。</p>
<p>这不包括由&amp;quot;可恢复项目&amp;quot;清理或系统清理终止期限的项目。</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsExpiredByPersonalExpiryTag - 由于个人过期标记导致过期的项目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示由于保留策略中的个人标记而由托管文件夹助理使其过期（软删除或硬删除）的项目数。</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsMovedByDefaultArchiveTag - 由于默认存档标记导致移动的项目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示由于保留策略中的任何非个人（默认或系统）存档标记而由托管文件夹助理移动至存档的项目数。</p>
<p>这不包括通过&amp;quot;可恢复项目&amp;quot;清理移动至存档中&amp;quot;可恢复项目&amp;quot;文件夹的项目。</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsMovedByPersonalArchiveTag - 由于存档标记导致移动的项目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示由于保留策略中的个人存档标记而由托管文件夹助理移动至存档的项目数。</p></td>
</tr>
<tr class="odd">
<td><p>TotalMovedDumpsterItems - 邮箱转储程序移动的项目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指示通过&amp;quot;可恢复项目&amp;quot;清理移动至存档中&amp;quot;可恢复项目&amp;quot;文件夹的项目数。</p></td>
</tr>
</tbody>
</table>

