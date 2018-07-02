---
title: '托管可用性: Exchange 2013 Help'
TOCTitle: 托管可用性
ms:assetid: ceb99e6f-6dca-446d-abfb-3e6fc6a72704
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn482056(v=EXCHG.150)
ms:contentKeyID: 59890410
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 托管可用性

 

_**适用于：**Exchange Online, Exchange Server 2013 SP1_

_**上一次修改主题：**2017-03-29_

确保用户获得良好的电子邮件体验一直是邮件系统管理员的主要目标。为了帮助确保 Microsoft Exchange Server 2013 组织的可用性和可靠性，必须主动监控系统的所有方面，且必须快速解决检测到的任何问题。在 Exchange 以前的版本中，监控关键系统组件通常涉及使用外部应用程序（如 Microsoft System Center 2012 Operations Manager）收集数据，以及针对在分析收集数据时检测到的问题提供恢复操作。Exchange 2010 和以前版本包括管理包形式的运行状况显示和相关性引擎。这些组件使 Operations Manager 能够确定某一特定组件是否正常运行。此外，Operations Manager 还使用 Exchange 2010 的内置诊断 cmdlet 基础结构对系统的多个方面运行综合事务。

Exchange 2013 采用了一种新方法，即，使用名为*托管可用性*、提供内置监控和恢复操作的功能来在本地监控和维护最终用户体验。

## 托管可用性

托管可用性也称为*主动监控*或*本地主动监控*，它是内置监控和恢复操作与 Exchange 高可用性平台的集成。它设计用于在问题出现后立即被系统检测到以检测并恢复。与 Exchange 之前的外部监视解决方案和技术不同的是，托管可用性不会尝试识别或沟通问题的根本原因。与此相反，它将专注于处理用户体验的三个关键方面的恢复部分：

  - **可用性**   用户是否可以访问该服务？

  - **延迟**   用户的体验如何？

  - **错误**   用户能否完成所需操作？

Exchange 2013 中的服务器角色合并和其他体系结构更改要求对 Exchange 以前版本中使用的监控方法和运行状况模型采用一种新方法。托管可用性设计通过提供本机运行状况监控和恢复解决方案来解决这些更改。它不再监控系统的单个单独块，而是监控端到端用户体验，并通过以恢复为主的操作保护最终用户的体验。

托管可用性是在每个 Exchange 2013 服务器上运行的内部进程。它每秒轮询和分析数百个运行状况度量。如果发现错误，大部分时候会自动修复。但始终会有一些托管可用性无法自行修复的问题。在这些情况下，托管可用性将通过事件日志记录将问题上报给管理员。

托管可用性以两种服务形式实现：

  - **Exchange 运行状况管理器服务 (MSExchangeHMHost.exe)**   这是用于管理工作进程的控制器进程。它用于在必要时构建、执行并启动和结束进程。它还用于在进程失败的情况下恢复工作进程，以防止工作进程出现单点故障。

  - **Exchange 运行状况管理器工作进程 (MSExchangeHMWorker.exe)**   这是在托管可用性框架中负责执行运行时任务的工作进程。

托管可用性使用永久存储执行其功能：

  - \\bin\\Monitoring\\config 文件夹中的 XML 文件用于存储某些探测器和监视器工作项目的配置设置。

  - Active Directory 用于存储全局覆盖。

  - Windows 注册表用于存储运行时数据，如书签和本地（服务器特定）覆盖。

  - Windows crimson 通道事件日志基础结构用于存储工作项目结果。

  - 运行状况邮箱用于探测活动。将在服务器上存在的每个邮箱数据库上创建多个运行状况邮箱。

如同下图中所示，托管可用性包括三个持续运行的主要异构组件。

**托管可用性组件**

![Exchange Server 2013 中的托管可用性](images/Dn482056.7a54dcb5-1e28-4bd4-87e6-0d496b4ab796(EXCHG.150).gif "Exchange Server 2013 中的托管可用性")

第一个组件称为\&quot;探测器\&quot;。探测器负责在服务器上进行测量并收集数据。这些测量结果将流入第二个组件，即\&quot;监视程序\&quot;。监视器包含系统基于在收集的数据上被视为正常的内容而使用的所有业务逻辑。类似于模式识别引擎，监视器将在收集的测量上寻找各种不同的模式，然后决定组件是否正常运行。最后，还有负责恢复和升级操作的\&quot;响应程序\&quot;。当某个组件未正常运行时，首先执行的操作是尝试恢复该组件。这可以包含多阶段恢复操作（例如，第一个尝试可以是重新启动应用程序池，第二个尝试可以是重新启动服务，第三个尝试可以是重新启动服务器，后续尝试可以是使服务器脱机以便它不再接受流量）。如果恢复操作不成功，系统将通过事件日志通知将问题上报给用户。

探测器有三个主要类别：反复探测器、通知探测器和检查探测器。反复探测器是系统进行的合成事务，以测试端到端用户体验。检查是执行性能数据收集的基础结构，包括用户流量，并使用设定的阈值测量收集的数据以确定用户故障的尖峰。这样，检查基础结构便能在用户遇到问题时意识到出现问题。最后，通知逻辑允许系统基于关键事件立即采取行动，而无需等待探测器收集的数据结果。这些通常是无需大量样本集即可检测和识别的例外或条件。

反复探测器每隔几分钟运行一次，并检查服务运行状况的某些方面。这些探测器可以通过 Exchange ActiveSync 将电子邮件发送到监视邮箱，它们可能会连接到 RPC 终结点，或者可能会验证\&quot;客户端访问到邮箱\&quot;的连接。

所有探测器都在 Microsoft.Exchange.ActiveMonitoring\\ProbeDefinition crimson 通道中的运行状况管理器服务启动上定义。每个探测器的定义都有许多属性，但最相关的属性是：

  - **Name** 探测器的名称，它以探测器的监视器的 *SampleMask* 作为开头。

  - **TypeName** 包含探测器逻辑的探测器的代码对象类型。

  - **ServiceName** 包含此探测器的运行状况集的名称。

  - **TargetResource** 探测器正在验证的对象。它是在执行变为探测结果 *ResultName* 时，附加到探测器名称中的。

  - **RecurrenceIntervalSeconds** 探测器的执行频率。

  - **TimeoutSeconds** 探测器在失败前将等待的时间。

有几百个反复探测器。这些探测器中有许多都是以单个数据库为基础，所以随着数据库数量的增加，探测器的数量也随之增长。大多数探测器都是在代码中定义的，因此不能直接找到。

反复探测器的基础知识如下所示：启动每个 *RecurrenceIntervalSeconds*，并检查（或探测）某些方面的运行状况。如果组件运行状况良好，则探测器将判定为合格，并将信息性事件传入或写入 *ResultType* 为 3 的 Microsoft.Exchange.ActiveMonitoring\\ProbeResult 通道。如果检查失败或者超时，探测器将判定为故障，并将错误事件写入同一通道。*ResultType* 为 4 表示检查未通过，*ResultType* 为 1 表示超时。如果超时，达到 *MaxRetryAttempts* 属性的值，则许多探测器将重新运行。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>注意</strong> ProbeResult crimson 通道会因为处理数百个每隔几分钟运行一次的探测器以及记录事件而变得非常繁忙，因此如果您对生产环境中的事件日志尝试高成本的查询时，会对您的 Exchange 服务器性能产生真正的影响。</td>
</tr>
</tbody>
</table>


通知是指不是由运行状况管理器框架运行的，而是由服务器上的一些其他服务运行的探测器。这些服务自行执行监测，然后通过直接写入探测结果将数据反馈到托管可用性框架中。在 ProbeDefinition 通道中无法看到这些探测器，因为该通道只描述由托管可用性框架运行的探测器。例如，ServerOneCopyMonitor 监视器由 MSExchangeDAGMgmt 服务写入的探测结果触发。该服务执行自己的监视，确定是否有问题，并记录探测结果。大多数通知探测器必须能够记录导致监视器不正常的红色事件，以及使监视器重新恢复正常的绿色事件。

检查探测器只在性能计数器高于或低于定义的阈值时才会记录事件。实际上，它们是通知探头的一种特殊情况，因为当达到配置的阈值时，将有服务监视服务器上的性能计数器，并将事件记录到 ProbeResult 通道。

若要找到被视为不正常的计数器和阈值，您可以查看监视器找到此检查探测器。*Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueAboveThresholdMonitor* 或 *Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueBelowThresholdMonitor* 类型的监视器意味着他们查看的探测器是检查探测器

监视器将查询探测器收集的数据，以基于预先定义的规则集确定是否需要采取措施。根据规则或问题本质的不同，监视器能够启动响应器或通过事件日志条目将问题上报给用户。此外，监视器将定义在出现故障后执行响应器的时间长度，以及恢复操作的工作流程。监视器具有各种状态。从系统状态角度来说，监视器具有两种状态：

  - **正常运行** 监视器正常运行，且收集的所有指标均在正常运行参数内。

  - **未正常运行**   监视器未正常运行，同时已通过响应器启动恢复或通过升级通知管理员。

从管理角度来说，监视器将在命令行管理程序中显示其他状态：

  - **降级**   当监视器处于未正常运行状态时间为 0 至 60 秒时，被视为降级。如果监视器处于未正常运行状态超过 60 秒，则被视为未正常运行。

  - **禁用**   管理员显式禁用监视器。

  - **不可用**   Microsoft Exchange 运行状况服务将定期查询每个监视器的状态。如果查询未得到响应，监视器状态将变为不可用。

  - **正在维修**   管理员设置\&quot;正在维修\&quot;状态向系统指示有人正在对系统采取纠正措施，这允许系统和人员将其他故障与同一时间正在采取的纠正措施（如数据库副本重新设定种子操作）区分开来。

每个监视器在其定义中都有一个 *SampleMask* 属性。监视器在执行时，都会在与监视器的 *SampleMask* 匹配的 *ResultName* 所在的 ProbeResult 通道中查找事件。这些事件可能来自反复探测器、通知探测器或检查探测器。如果达到了探测器的阈值，则会出现不正常状况。从监视器的角度看，所有三个探测器类型与它们每个登录到 ProbeResult 通道的类型是一样。

值得一提的是，单个探测器故障并不一定表明服务器出了问题。监视器旨在能够正确地识别何时出现真正需要修复的问题。这就是为什么许多监视器在不正常情况出现之前对很多探测器故障设置了阈值的原因。即使这样，许多问题都可以通过响应程序自动进行修复，所以查找需要人工干预的问题的最好去处是 Microsoft.Exchange.ManagedAvailability\\Monitoring crimson 通道。这将包括最新的探测器错误。

顾名思义，响应器对监视器生成的警报执行某些类型的响应。响应器执行多种恢复操作，如将应用程序工作池重置为重新启动服务器。有多种类型的响应器：

  - **重新启动响应器** 终止并重新启动服务

  - **重置应用程序池响应器** 在 Internet 信息服务 (IIS) 中停止并重新启动应用程序池

  - **故障转移响应器** 启动数据库或服务器故障转移

  - **缺陷检查响应器** 启动服务器缺陷检查，从而导致服务器重新启动

  - **脱机响应器** 使服务器上的协议停止运行（拒绝客户端请求）

  - **联机响应器** 使服务器上的某个协议重新运行（接受客户端请求）

  - **上报响应器** 通过事件日志记录将问题上报给管理员

除了上面列出的响应器，某些组件也有自己独特的专用响应器。

所有响应器（包括限制行为）均提供用于控制响应器操作的内置排序机制。限制行为设计为确保系统不会由于响应器恢复操作而受损害或变得更糟。所有响应器均会以某种方式进行限制。限制发生时，可能会跳过或延迟响应器恢复操作，这取决于响应器操作。例如，当限制缺陷检查响应器时，其操作将被跳过，而不是延迟。

## 运行状况设置

从报告的角度来看，托管可用性具有两个运行状况视图，一个内部视图和一个外部视图。内部视图使用*运行状况设置*。Exchange 2013 中的每个组件（例如 Outlook Web App、Exchange ActiveSync、信息存储服务、内容索引、传输服务，等等）由托管可用性使用探测器、监视器和响应器进行监控。给定组件的一组探测器、监视器和响应器称为*运行状况设置*。运行状况设置是一组探测器、监视器和响应器，用于确定该组件是否正常运行。运行状况设置的当前状态（例如是否正常运行）通过运行状况设置监视器的状态确定。如果运行状况设置的所有监视器均正常运行，则说明运行状况设置处于正常状态。如果任何监视器不处于正常状态，则运行状况设置状态由最差的监视器决定。

有关查看服务器运行状况或运行状况设置状态的详细步骤，请参阅[管理运行状况设置和服务器运行状况](manage-health-sets-and-server-health-exchange-2013-help.md)。

## 运行状况组

托管可用性的外部视图由*运行状况组*组成。运行状况组向 System Center Operations Manager 2007 R2 和 System Center Operations Manager 2012 公开。

有四个主要的运行状况组：

  - **客户触点** 影响实时用户交互的组件，如协议或信息存储

  - **服务组件** 没有直接的实时用户交互的组件，例如 Microsoft Exchange 邮箱复制服务或脱机通讯簿生成过程 (OABGen)

  - **服务器组件** 服务器的物理资源，如磁盘空间、内存和网络连接

  - **依赖项可用性** 服务器访问所需依赖项的功能，如 Active Directory、DNS，等等。

安装 Exchange 管理包时，系统中心操作管理器 (SCOM) 作为健康门户网站来查看与Exchange环境相关的信息。SCOM 仪表板包括Exchange服务器健康状态的三个视图︰

  - **活动警报** 上报响应器将事件写入 Windows 事件日志中，由 SCOM 内的监视器使用。这些事件在\&quot;活动警报\&quot;视图中显示为警报。

  - **组织运行状况** Exchange 组织运行状况的整体运行状况汇总摘要将显示在此视图中。这些汇总包括显示单个数据库可用性组的运行状况以及特定 Active Directory 站点内的运行状况。

  - **服务器运行状况** 相关的运行状况设置组合到运行状况组并汇总在此视图中。

## 覆盖

覆盖使管理员能够配置托管可用性探测器、监视器和响应器的某些方面。覆盖可用于微调托管可用性使用的一些阈值。覆盖可用于对意外事件启用紧急操作，这可能需要不同于现成默认设置的配置设置。

可以创建覆盖并将其应用于单个服务器（称为*服务器覆盖*），也可将其应用于一组服务器（称为*全局覆盖*）。服务器覆盖配置数据存储在覆盖应用的服务器上的 Windows 注册表中。全局覆盖配置数据存储在 Active Directory 中。

覆盖可以配置为无限期持续，或将它们配置为特定的持续时间。此外，全局覆盖可以配置为应用于所有服务器，或仅应用于运行 Exchange 特定版本的服务器。

配置覆盖时，它不会立即生效。Microsoft Exchange 运行状况管理器服务每隔 10 分钟检查一次更新的配置数据。此外，全局覆盖依赖于 Active Directory 复制延迟。

有关查看或配置服务器覆盖或全局覆盖的详细步骤，请参阅[配置托管可用性覆盖](configure-managed-availability-overrides-exchange-2013-help.md)。

## 管理任务和 Cmdlet

对于托管可用性，管理员通常需执行三个主要操作任务：

  - 提取或查看系统运行状况

  - 查看运行状况设置以及探测器、监视器和响应器的相关详细信息

  - 管理覆盖

托管可用性的两个主要管理工具是 Windows 事件日志和命令行管理程序。托管可用性在 Exchange ActiveMonitoring 和 ManagedAvailability crimson 通道事件日志中记录大量信息，例如：

  - 探测器、监视器和响应器定义，记录在各自的\*定义事件日志中。

  - 探测器、监视器和响应器结果，记录在各自的\*结果事件日志中。

  - 有关响应器恢复操作的详细信息，包括何时启动恢复操作、何时视为完成（是否成功）以及哪些操作记录在 RecoveryActionResults 事件日志中。

有 12 个 cmdlet 用于托管可用性，如下表所示。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/jj218703(v=exchg.150)">Get-ServerHealth</a></p></td>
<td><p>用于获取原始服务器的运行状况信息，例如运行状况设置及其当前状态（是否正常）、运行状况设置监视器、服务器组件、探测器的目标资源，以及与探测器或监视器启动或停止时间和状态转换时间有关的时间戳。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/jj218724(v=exchg.150)">Get-HealthReport</a></p></td>
<td><p>用于获取运行状况摘要视图，其中包括运行状况设置及其当前状态。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/jj218668(v=exchg.150)">Get-MonitoringItemIdentity</a></p></td>
<td><p>用于查看与特定运行状况设置相关的探测器、监视器和响应器。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/jj218642(v=exchg.150)">Get-MonitoringItemHelp</a></p></td>
<td><p>用于查看有关探测器、监视器和响应器的某些属性的说明。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/jj218628(v=exchg.150)">Add-ServerMonitoringOverride</a></p></td>
<td><p>用于创建探测器、监视器或响应器的特定于服务器的局部覆盖。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/jj218664(v=exchg.150)">Get-ServerMonitoringOverride</a></p></td>
<td><p>用来查看指定服务器上的局部覆盖的列表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/dn482411(v=exchg.150)">Remove-ServerMonitoringOverride</a></p></td>
<td><p>用于从特定服务器删除局部覆盖。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/jj218683(v=exchg.150)">Add-GlobalMonitoringOverride</a></p></td>
<td><p>用于为一组服务器创建全局覆盖。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/jj218627(v=exchg.150)">Get-GlobalMonitoringOverride</a></p></td>
<td><p>用于查看在组织中配置的全局覆盖的列表。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/jj218675(v=exchg.150)">Remove-GlobalMonitoringOverride</a></p></td>
<td><p>用于删除全局覆盖。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/jj218699(v=exchg.150)">Set-ServerComponentState</a></p></td>
<td><p>用于配置一个或多个服务器组件的状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/jj218713(v=exchg.150)">Get-ServerComponentState</a></p></td>
<td><p>用于查看一个或多个服务器组件的状态。</p></td>
</tr>
</tbody>
</table>

