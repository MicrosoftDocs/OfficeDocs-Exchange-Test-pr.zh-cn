---
title: '监视数据库可用性组: Exchange 2013 Help'
TOCTitle: 监视数据库可用性组
ms:assetid: f5bdfd6e-e93c-4d96-8bc2-548750d51930
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351258(v=EXCHG.150)
ms:contentKeyID: 50491990
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 监视数据库可用性组

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

针对数据库可用性组 (DAG)、诊断信息收集和低磁盘空间监视阈值配置，您可以使用此主题中的详细信息监视邮箱数据库副本运行状况和状态。

## Get-MailboxDatabaseCopyStatus cmdlet

可以使用 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-cn/library/dd298044\(v=exchg.150\)) cmdlet 查看关于邮箱数据库副本的状态信息。通过此 cmdlet，您可以查看有关特定数据库的所有副本的信息、有关特定服务器上数据库的特定副本的信息，或者有关服务器上所有数据库副本的信息。下表介绍了邮箱数据库副本的副本状态的可能值。

### 数据库副本状态

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>数据库副本状态</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Failed</p></td>
<td><p>邮箱数据库副本因未挂起而处于&amp;quot;失败&amp;quot;状态，并且该副本无法复制或重播日志文件。当邮箱数据库副本处于&amp;quot;失败&amp;quot;状态并且未挂起时，系统将定期检查导致副本状态更改为&amp;quot;失败&amp;quot;的问题是否已得到解决。当系统检测到该问题已得到解决后，并且没有其他任何问题，则副本状态将自动更改为&amp;quot;正常&amp;quot;。</p></td>
</tr>
<tr class="even">
<td><p>Seeding</p></td>
<td><p>正在为邮箱数据库副本设定种子或正在为邮箱数据库副本的内容索引设定种子，或两者兼有。成功设定种子后，副本状态将改为&amp;quot;正在初始化&amp;quot;。</p></td>
</tr>
<tr class="odd">
<td><p>SeedingSource</p></td>
<td><p>正在将邮箱数据库副本用作数据库副本种子设定操作的源。</p></td>
</tr>
<tr class="even">
<td><p>Suspended</p></td>
<td><p>由于管理员通过运行 <strong>Suspend-MailboxDatabaseCopy</strong> cmdlet 手动挂起数据库副本，所以该邮箱数据库副本处于&amp;quot;已挂起&amp;quot;状态。</p></td>
</tr>
<tr class="odd">
<td><p>Healthy</p></td>
<td><p>邮箱数据库副本正在成功复制和重播日志文件，或者已成功复制和重播所有可用日志文件。</p></td>
</tr>
<tr class="even">
<td><p>ServiceDown</p></td>
<td><p>Microsoft Exchange 复制服务不可用或未在驻留有邮箱数据库副本的服务器上运行。</p></td>
</tr>
<tr class="odd">
<td><p>Initializing</p></td>
<td><p>邮箱数据库副本在下列情况下处于&amp;quot;Initializing&amp;quot;状态：创建数据库副本后、Microsoft Exchange 复制服务正在启动或刚被启动时，以及从&amp;quot;Suspended&amp;quot;、&amp;quot;ServiceDown&amp;quot;、&amp;quot;Failed&amp;quot;、&amp;quot;Seeding&amp;quot;或&amp;quot;SinglePageRestore&amp;quot;转变为另一种状态的过程中。处于此状态时，系统将验证数据库和日志流是否处于一致状态。在大多数情况下，副本状态在&amp;quot;Initializing&amp;quot;状态下保持约 15 秒的时间，但在所有情况下，处于该状态的时间一般不会超过 30 秒。</p></td>
</tr>
<tr class="even">
<td><p>Resynchronizing</p></td>
<td><p>正在将邮箱数据库副本及其日志文件与数据库的活动副本进行比较，以检查两个副本之间是否存在任何差异。副本将保持此状态，直到检测到任何差异并且加以解决。</p></td>
</tr>
<tr class="odd">
<td><p>Mounted</p></td>
<td><p>活动副本处于联机状态并接受客户端连接。只有邮箱数据库的活动副本才能具有&amp;quot;Mounted&amp;quot;状态。</p></td>
</tr>
<tr class="even">
<td><p>Dismounted</p></td>
<td><p>活动副本处于脱机状态并且不接受客户端连接。只有邮箱数据库的活动副本才能具有&amp;quot;Dismounted&amp;quot;状态。</p></td>
</tr>
<tr class="odd">
<td><p>Mounting</p></td>
<td><p>活动副本即将联机，但尚未接受客户端连接。只有邮箱数据库副本的活动副本才能具有&amp;quot;Mounting&amp;quot;副本状态。</p></td>
</tr>
<tr class="even">
<td><p>Dismounting</p></td>
<td><p>活动副本即将脱机并将终止客户端连接。只有邮箱数据库副本的活动副本才能具有&amp;quot;Dismounting&amp;quot;副本状态。</p></td>
</tr>
<tr class="odd">
<td><p>DisconnectedAndHealthy</p></td>
<td><p>邮箱数据库副本不再连接到活动数据库副本，并且在丢失连接时邮箱数据库副本处于&amp;quot;Healthy&amp;quot;状态。此状态表示数据库副本与其源数据库副本的连接性。当源副本和目标数据库副本之间出现 DAG 网络故障时可能会报告该状态。</p></td>
</tr>
<tr class="even">
<td><p>DisconnectedAndResynchronizing</p></td>
<td><p>邮箱数据库副本不再连接到活动数据库副本，并且在丢失连接时邮箱数据库副本处于&amp;quot;Resynchronizing&amp;quot;状态。此状态表示数据库副本与其源数据库副本的连接性。当源副本和目标数据库副本之间出现 DAG 网络故障时可能会报告该状态。</p></td>
</tr>
<tr class="odd">
<td><p>FailedAndSuspended</p></td>
<td><p>由于检测到故障并且该故障的解决方案明确要求管理员进行干预，因此系统会同时设置&amp;quot;Failed&amp;quot;和&amp;quot;Suspended&amp;quot;状态。例如，系统检测到活动邮箱数据库和数据库副本之间存在不可恢复的差异。与&amp;quot;已失败&amp;quot;状态不同，系统不会定期检查该问题是否已解决以及自动恢复。而是必须由管理员进行干预以解决导致失败的根本原因，然后数据库副本才能过渡到正常状态。</p></td>
</tr>
<tr class="even">
<td><p>SinglePageRestore</p></td>
<td><p>此状态表示正在对邮箱数据库副本执行单页面还原操作。</p></td>
</tr>
</tbody>
</table>


**Get-MailboxDatabaseCopyStatus** cmdlet 也返回关于正在使用的复制网络的详细信息，包括 *IncomingLogCopyingNetwork*（针对被动数据库副本返回）和 *OutgoingConnections*（针对具有多个副本的活动数据库以及任何用作数据库种子操作源的数据库副本而返回）。为文件模式复制中的数据库副本提供传出连接信息。不为块模式复制中的数据库副本提供传出连接信息。

## Get-MailboxDatabaseCopyStatus 示例

以下示例使用 **Get-MailboxDatabaseCopyStatus** cmdlet。每个示例都将结果传输到 **Format-List** cmdlet 以便按列表格式显示输出内容。

本示例将返回 DB2 数据库的所有副本的状态信息。

```powershell
Get-MailboxDatabaseCopyStatus -Identity DB2 | Format-List
```

本示例将返回邮箱服务器 MBX2 上的所有数据库副本的状态。

```powershell
Get-MailboxDatabaseCopyStatus -Server MBX2 | Format-List
```

本示例将返回本地邮箱服务器上的所有数据库副本的状态。

```powershell
Get-MailboxDatabaseCopyStatus -Local | Format-List
```

有关使用 **Get-MailboxDatabaseCopyStatus** cmdlet 的详细信息，请参阅 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-cn/library/dd298044\(v=exchg.150\))。

## Test-ReplicationHealth cmdlet

可以使用 [Test-ReplicationHealth](https://technet.microsoft.com/zh-cn/library/bb691314\(v=exchg.150\)) cmdlet 查看关于邮箱数据库副本的连续复制状态信息。此 cmdlet 可用于检查复制和重播状态的各个方面，以提供有关 DAG 中的特定邮件服务器的完整概述。

设计 **Test-ReplicationHealth** cmdlet 是为了主动监视连续复制和连续复制管道、Active Manager 的可用性，以及基础群集服务、仲裁和网络组件的运行状况和状态。可以在 DAG 中的任何邮箱服务器上本地或远程运行该 cmdlet。**Test-ReplicationHealth** cmdlet 将执行在下表中列出的测试。

### Test-ReplicationHealth cmdlet 测试

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>测试名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ClusterService</p></td>
<td><p>验证群集服务是否正在指定的 DAG 成员或本地服务器（如果未指定 DAG 成员）上运行并且可访问。</p></td>
</tr>
<tr class="even">
<td><p>ReplayService</p></td>
<td><p>验证 Microsoft Exchange 复制服务是否正在指定的 DAG 成员或本地服务器（如果未指定 DAG 成员）上运行并且可访问。</p></td>
</tr>
<tr class="odd">
<td><p>ActiveManager</p></td>
<td><p>验证在指定的 DAG 成员（如果未指定 DAG 成员，则为本地服务器）上运行的活动管理器实例是否是有效的角色（主要、辅助或单独）。</p></td>
</tr>
<tr class="even">
<td><p>TasksRpcListener</p></td>
<td><p>验证任务远程过程调用 (PRC) 服务器是否正在指定的 DAG 成员或本地服务器（如果未指定 DAG 成员）上运行并且可访问。</p></td>
</tr>
<tr class="odd">
<td><p>TcpListener</p></td>
<td><p>验证 TCP 日志副本侦听程序是否正在指定的 DAG 成员或本地服务器（如果未指定 DAG 成员）上运行并且可访问。</p></td>
</tr>
<tr class="even">
<td><p>ServerLocatorService</p></td>
<td><p>在 DAG 成员和客户端访问服务器上，验证在 Active Directory 和活动管理器中执行查找的活动管理器客户端/服务器进程，以确定用户邮箱数据库是否处于活动状态。</p></td>
</tr>
<tr class="odd">
<td><p>DagMembersUp</p></td>
<td><p>验证所有 DAG 成员是否均可用、正在运行并且可访问。</p></td>
</tr>
<tr class="even">
<td><p>ClusterNetwork</p></td>
<td><p>验证指定的 DAG 成员（如果未指定 DAG 成员，则为本地服务器）上的所有群集管理的网络是否均可用。</p></td>
</tr>
<tr class="odd">
<td><p>QuorumGroup</p></td>
<td><p>验证默认的群集组（仲裁组）是否处于正常和联机状态。</p></td>
</tr>
<tr class="even">
<td><p>FileShareQuorum</p></td>
<td><p>验证为 DAG 配置的见证服务器、见证目录和共享是否可访问。</p></td>
</tr>
<tr class="odd">
<td><p>DatabaseRedundancy</p></td>
<td><p>验证在指定的 DAG 成员或本地服务器（如果未指定 DAG 成员）上是否至少有一个可用的数据库健全副本。</p></td>
</tr>
<tr class="even">
<td><p>DatabaseAvailability</p></td>
<td><p>验证指定的 DAG 成员或本地服务器（如果未指定 DAG 成员）上的数据库是否具有充分的可用性。</p></td>
</tr>
<tr class="odd">
<td><p>DBCopySuspended</p></td>
<td><p>检查指定的 DAG 成员（如果未指定 DAG 成员，则为本地服务器）上的任何邮箱数据库副本是否处于&amp;quot;Suspended&amp;quot;状态。</p></td>
</tr>
<tr class="even">
<td><p>DBCopyFailed</p></td>
<td><p>检查指定的 DAG 成员（如果未指定 DAG 成员，则为本地服务器）上的任何邮箱数据库副本是否处于&amp;quot;Failed&amp;quot;状态。</p></td>
</tr>
<tr class="odd">
<td><p>DBInitializing</p></td>
<td><p>检查指定的 DAG 成员（如果未指定 DAG 成员，则为本地服务器）上的任何邮箱数据库副本是否处于&amp;quot;Initializing&amp;quot;状态。</p></td>
</tr>
<tr class="even">
<td><p>DBDisconnected</p></td>
<td><p>检查指定 DAG 成员（如果未指定 DAG 成员，则为本地服务器）上的任何邮箱数据库副本是否处于&amp;quot;Disconnected&amp;quot;状态。</p></td>
</tr>
<tr class="odd">
<td><p>DBLogCopyKeepingUp</p></td>
<td><p>验证指定的 DAG 成员（如果未指定 DAG 成员，则为本地服务器）上的数据库被动副本的日志复制和检查活动是否可以跟上活动副本上的日志生成活动。</p></td>
</tr>
<tr class="even">
<td><p>DBLogReplayKeepingUp</p></td>
<td><p>验证指定的 DAG 成员（如果未指定 DAG 成员，则为本地服务器）上的数据库被动副本重播活动是否可以跟上日志复制和检查活动。</p></td>
</tr>
</tbody>
</table>


## Test-ReplicationHealth 示例

本示例使用 **Test-ReplicationHealth** cmdlet 测试邮箱服务器 MBX1 的复制的运行状况。

```powershell
Test-ReplicationHealth -Identity MBX1
```

## Crimson 通道事件日志记录

Windows 包括两个类别的事件日志：Windows 日志、应用程序和服务日志。Windows 日志类别包括之前版本的 Windows 提供的事件日志：应用程序、安全和系统事件日志。它还包括两种新日志：Setup 日志和 ForwardedEvents 日志。Windows 日志用于存储来自旧版应用程序的事件以及适用于整个系统的事件。

应用程序和服务日志是一类新的事件日志。这些日志存储来自单个应用程序或组件的事件，而不存储可能影响整个系统的事件。此新事件日志类别被称为应用程序的 crimson 通道。

应用程序和服务日志类别包括四个子类型：管理日志、操作日志、分析日志和调试日志。如果您使用事件日志记录对问题进行故障排除，则可能会对管理日志中的事件特别感兴趣。管理日志中的事件将提供有关如何对事件做出响应的指导。操作日志中的事件也很有用，但可能需要更多的解释。管理日志和调试日志并不那么用户友好。分析日志（默认情况下被隐藏和禁用）将存储跟踪问题的事件，并且通常会记录大量事件。调试日志由开发人员在调试应用程序时使用。

Exchange 2013 会将事件记录到应用程序和服务日志区域内的 crimson 通道。可以通过执行下列步骤来查看这些通道：

1.  打开事件查看器。

2.  在控制台树中，导航到\&quot;应用程序和服务日志\&quot;\>\&quot;Microsoft\&quot;\>\&quot;Exchange\&quot;。

3.  在 **Exchange** 下方，选择一个 crimson 通道（如\&quot;HighAvailability\&quot;或\&quot;MailboxDatabaseFailureItems\&quot;）查看 DAG 和数据库副本相关事件，或选择\&quot;ActiveMontoring\&quot;或\&quot;ManagedAvailability\&quot;查看托管可用性相关事件。

HighAvailability 通道包含有关 Microsoft Exchange 复制服务的启动和关闭的事件，以及有关在 Microsoft Exchange 复制服务中运行的各种组件（例如 Active Manager、第三方同步复制 API、任务 PRC 服务器、TCP 侦听程序和卷影复制服务 (VSS) 编写器）的事件。HighAvailability 通道还可由 Active Manager 用于记录与 Active Manager 角色监视相关的事件和数据库操作事件（例如数据库装入操作和日志截断），以及记录与 DAG 基础群集相关的事件。

MailboxDatabaseFailureItems 通道可用于记录与会影响复制的邮箱数据库的故障相关的事件。

ActiveMonitoring 通道包含托管可用性探测、监视和响应程序的定义和结果事件。

ManagedAvailability 通道包含恢复操作日志和结果以及相关事件。

## 低磁盘空间监视器

Exchange 2013 托管可用性每分钟监视数百个系统指标和组件，包括邮箱服务器角色所用卷上的可用磁盘空间量。Exchange 2013 Service Pack 1 (SP1) 之前的版本中，Exchange 监视所有本地卷上的可用空间，包括不含有数据库或日志文件的卷。在 SP1 和更高版本中，仅监控包含 Exchange 数据库和日志文件的卷。在 SP1 中，低容量空间监视器的默认阈值为 200 GB。在 Exchange 2013 累计更新 6 和更高版本中，默认阈值为 180 GB。在 SP1 和更高版本中，通过在每个需要自定义的邮箱服务器上添加以下 DWORD 注册表值（以 MB 为单位）可以配置阈值：

路径：** HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters**

值：*SpaceMonitorLowSpaceThresholdInMB*

例如，若要配置阈值为 100 GB，您需配置以下注册表值：

**REG\_DWORD 186a0 (100000)**

配置或修改以上注册表值后，必须重启 Microsoft Exchange DAG 管理服务以使更改生效。

## CollectOverMetrics.ps1 脚本

Exchange 2013 包括名为 CollectOverMetrics.ps1 的脚本，此脚本位于\&quot;脚本\&quot;文件夹中。CollectOverMetrics.ps1 读取 DAG 成员事件日志来收集特定时段内有关数据库操作（如数据库装入、移动和故障转移）的信息。对于每个操作，该脚本记录以下信息：

  - 数据库的标识

  - 操作的起止时间

  - 操作开始和结束时装入数据库的服务器

  - 操作的原因

  - 操作是否成功；如果操作失败，将包含错误详细信息

该脚本将此信息写入 .csv 文件，每行对应一个操作。每个 DAG 对应一个单独的 .csv 文件。

该脚本支持允许您自定义脚本行为和输出内容的参数。例如，通过使用 *Database* 或 *ReportFilter* 参数，可以将结果限制为一个指定的子集。只有与这些筛选器相匹配的操作才会包含在 HTML 摘要报告中。下表列出了可用的参数。

### CollectOverMetrics.ps1 脚本参数

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DatabaseAvailabilityGroup</em></p></td>
<td><p>指定要从中收集指标的 DAG 的名称。如果省略此参数，则会使用本地服务器所属的 DAG。可以使用通配符从多个 DAG 收集信息以及生成多个 DAG 的报告。</p></td>
</tr>
<tr class="even">
<td><p><em>Database</em></p></td>
<td><p>提供需要为其生成报告的数据库的列表。支持通配符字符，例如 <code>-Database:&quot;DB1&quot;,&quot;DB2&quot;</code> 或 <code>-Database:&quot;DB*&quot;</code>。</p></td>
</tr>
<tr class="odd">
<td><p><em>StartTime</em></p></td>
<td><p>指定要报告的时段的持续时间。该脚本仅收集这一期限内记录的事件。因此，该脚本可能只捕获部分操作记录（例如，只有该时段开始时某个操作的结束信息，或反过来）。如果 <em>StartTime</em> 和 <em>EndTime</em> 均未指定，脚本会默认将该时段指定为过去 24 小时。如果仅指定其中一个参数，则该时段将为指定时间之前或之后的 24 小时。</p></td>
</tr>
<tr class="even">
<td><p><em>EndTime</em></p></td>
<td><p>指定要报告的时段的持续时间。该脚本仅收集这一期限内记录的事件。因此，该脚本可能只捕获部分操作记录（例如，只有该时段开始时某个操作的结束信息，或反过来）。如果 <em>StartTime</em> 和 <em>EndTime</em> 均未指定，脚本会默认将该时段指定为过去 24 小时。如果仅指定其中一个参数，则该时段将为指定时间之前或之后的 24 小时。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>指定用于存储事件处理结果的文件夹。如果省略此参数，将使用&amp;quot;脚本&amp;quot;文件夹。指定此参数后，脚本将获取由该脚本生成的 .csv 文件的列表，并使用这些文件作为源数据来生成 HTML 摘要报告。该报告与使用 -GenerateHtmlReport 选项生成的报告相同。可以在许多不同时间，甚至是在重叠的时间跨多个 DAG 生成文件，并且脚本会将所有文件的数据合并在一起。</p></td>
</tr>
<tr class="even">
<td><p><em>GenerateHtmlReport</em></p></td>
<td><p>指定脚本收集其记录的所有信息，按操作类型对数据进行分组，然后生成包含每个组的统计信息的 HTML 文件。报告中包含每个组的操作总数、失败的操作数以及每个组中的操作所用时间的统计信息。报告中还包含导致操作失败的错误类型的细目。</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowHtmlReport</em></p></td>
<td><p>指定对于以 HTML 生成的报告，生成后应在 Web 浏览器中显示。</p></td>
</tr>
<tr class="even">
<td><p><em>SummariseCsvFiles</em></p></td>
<td><p>指定脚本从其之前生成的现有 .csv 文件中读取数据。然后使用此数据生成摘要报告，该报告与 <em>GenerateHtmlReport</em> 参数生成的报告类似。</p></td>
</tr>
<tr class="odd">
<td><p><em>ActionType</em></p></td>
<td><p>指定脚本应该收集的操作类型。此参数的值包括 <code>Move</code>、<code>Mount</code>、<code>Dismount</code> 和 <code>Remount</code>。<code>Move</code> 值是指数据库更改其活动服务器（无论是通过控制移动还是故障转移）的任何一次操作。<code>Mount</code>、<code>Dismount</code> 和 <code>Remount</code> 值是指数据库更改其装入状态而未移到另一台计算机的操作。</p></td>
</tr>
<tr class="even">
<td><p><em>ActionTrigger</em></p></td>
<td><p>指定脚本应该收集的管理操作。此参数的值为 <code>Admin</code> 或 <code>Automatic</code>。自动操作是指系统自动执行的操作（例如，服务器脱机时的故障转移）。管理操作是指管理员使用 Exchange 命令行管理程序或 Exchange 管理中心执行的所有操作。</p></td>
</tr>
<tr class="odd">
<td><p><em>RawOutput</em></p></td>
<td><p>指定脚本将原本要写入到 .csv 文件的结果直接写入输出流，就像使用 Write-Output 参数执行的操作一样。然后可以将此信息通过管道传递到其他命令。</p></td>
</tr>
<tr class="even">
<td><p><em>IncludedExtendedEvents</em></p></td>
<td><p>指定脚本收集提供装入数据库所用时间的诊断详细信息的事件。如果服务器上的应用程序事件日志很大，此过程可能会很耗时。</p></td>
</tr>
<tr class="odd">
<td><p><em>MergeCSVFiles</em></p></td>
<td><p>指定脚本收集包含有关每个操作的数据的 .csv 文件，并将这些文件合并为单个 .csv 文件。</p></td>
</tr>
<tr class="even">
<td><p><em>ReportFilter</em></p></td>
<td><p>指定对 .csv 文件中包含相应字段的操作应用筛选器。该参数使用与 <code>Where</code> 操作相同的格式，其中每个元素设为 <code>$_</code> 并且返回布尔值。例如：<code>{$_DatabaseName -notlike &quot;Mailbox Database*&quot;}</code> 可用于从报告中排除默认数据库。</p></td>
</tr>
</tbody>
</table>


## CollectOverMetrics.ps1 示例

以下示例收集名为 DAG1 的 DAG 中与 DB\*（包括通配符）匹配的所有数据库的指标。收集这些指标后，将生成并显示一个 HTML 报告。

    CollectOverMetrics.ps1 -DatabaseAvailabilityGroup DAG1 -Database:"DB*" -GenerateHTMLReport -ShowHTMLReport

以下示例说明可用于筛选 HTML 摘要报告的方法。第一个示例使用 *Database* 参数获取数据库名称的列表。从而使摘要报告仅包含有关这些数据库的数据。接下来的两个示例使用 *ReportFilter* 选项。最后一个示例筛选出所有默认数据库。

    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -Database MailboxDatabase123,MailboxDatabase456
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { $_.DatabaseName -notlike "Mailbox Database*" }
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { ($_.ActiveOnStart -like "ServerXYZ*") -and ($_.ActiveOnEnd -notlike "ServerXYZ*") }

## CollectReplicationMetrics.ps1 脚本

Exchange 2013 中包含的另一个运行状况指标脚本是 CollectReplicationMetrics.ps1。此脚本提供监视的活动表单，会在运行时实时收集指标。CollectReplicationMetrics.ps1 从与数据库复制相关的性能计数器中收集数据。该脚本从多个邮箱服务器中收集计数器数据，将每台服务器的数据写入 .csv 文件，然后综合使用所有这些数据报告各种统计信息（例如，每个副本出现故障或挂起的时长，复制队列或重播队列的平均长度，或副本不符合故障转移条件的时长）。

可以逐个指定服务器，也可以指定整个 DAG。可以运行脚本先收集数据，再生成报告，也可以仅收集数据或仅报告已收集的数据。可以指定数据取样的频率和收集数据的总持续时间。

从每台服务器收集的数据将写入名为 **CounterData.\<ServerName\>.\<TimeStamp\>.csv** 的文件。如果运行脚本时未使用 *DagName* 参数，则摘要报告将写入文件 **HaReplPerfReport.\<DAGName\>.\<TimeStamp\>.csv** 或 **HaReplPerfReport.\<TimeStamp\>.csv**。

脚本启动 Windows PowerShell 作业以从每台服务器收集数据。这些作业将在数据收集的整个时段内运行。如果指定大量服务器，此过程将占用相当大的内存。此过程的最后一个阶段是将数据整理成摘要报告，如果包含大量数据，该阶段也将花费大量时间。可以在某一台计算机上运行收集步骤，然后将数据复制到其他地方进行处理。

ollectReplicationMetrics.ps1 脚本支持允许您自定义脚本行为和输出内容的参数。下表列出了可用的参数。

### CollectReplicationMetrics.ps1 脚本参数

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>指定要从中收集指标的 DAG 的名称。如果省略此参数，则会使用本地服务器所属的 DAG。</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseNames</em></p></td>
<td><p>提供需要为其生成报告的数据库的列表。支持使用通配符，例如 <code>-DatabaseNames:&quot;DB1&quot;,&quot;DB2&quot;</code> 或 <code>-DatabaseNames:&quot;DB*&quot;</code>。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>指定用于存储事件处理结果的文件夹。如果省略此参数，将使用&amp;quot;脚本&amp;quot;文件夹。</p></td>
</tr>
<tr class="even">
<td><p><em>Duration</em></p></td>
<td><p>指定运行收集过程的时间段。典型值为 1 到 3 个小时。仅当每次取样之间时间间隔较长，或通过计划任务运行一系列较短作业时，才应使用更长的持续时间。</p></td>
</tr>
<tr class="odd">
<td><p><em>Frequency</em></p></td>
<td><p>指定收集数据指标的频率。典型值为 30 秒、1 分钟或 5 分钟。在正常情况下，如果使用小于这些值的时间间隔，每次取样之间的差别将不明显。</p></td>
</tr>
<tr class="even">
<td><p><em>Servers</em></p></td>
<td><p>指定从中收集统计信息的服务器的标识。可以指定包括通配符或 GUID 在内的任何值。</p></td>
</tr>
<tr class="odd">
<td><p><em>SummariseFiles</em></p></td>
<td><p>指定用于生成摘要报告的 .csv 文件列表。这些文件名为 <strong>CounterData.&lt;CounterData&gt;*</strong>，由 CollectReplicationMetrics.ps1 脚本生成。</p></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>指定脚本执行的处理过程。可以使用下列值：</p>
<ul>
<li><p><code>CollectAndReport</code>   此值为默认值。该值指示脚本应该从服务器收集数据，并处理这些数据以生成摘要报告。</p></li>
<li><p><code>CollectOnly</code>   该值指示脚本应仅收集数据，而不生成报告。</p></li>
<li><p><code>ProcessOnly</code>   该值指示脚本应该从一组 .csv 文件中导入数据，并处理这些数据以生成摘要报告。<em>SummariseFiles</em> 参数用于为脚本提供要处理的文件列表。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MoveFilestoArchive</em></p></td>
<td><p>指定脚本应该在处理完成后将文件移动到压缩文件夹。</p></td>
</tr>
<tr class="even">
<td><p><em>LoadExchangeSnapin</em></p></td>
<td><p>指定脚本应该加载命令行管理程序命令。当脚本需要在命令行管理程序之外（如，在计划任务中）运行时，该参数很有用。</p></td>
</tr>
</tbody>
</table>


## CollectReplicationMetrics.ps1 示例

以下示例从名为 DAG1 的 DAG 中的所有服务器收集一个小时的数据（取样时间间隔为 1 分钟），然后生成摘要报告。此外，由于使用了 *ReportPath* 参数，脚本会将所有文件置于当前目录中。

```powershell
CollectReplicationMetrics.ps1 -DagName DAG1 -Duration "01:00:00" -Frequency "00:01:00" -ReportPath
```

以下示例从与 CounterData\* 相匹配的所有文件读取数据，然后生成摘要报告。

    CollectReplicationMetrics.ps1 -SummariseFiles (dir CounterData*) -Mode ProcessOnly -ReportPath

