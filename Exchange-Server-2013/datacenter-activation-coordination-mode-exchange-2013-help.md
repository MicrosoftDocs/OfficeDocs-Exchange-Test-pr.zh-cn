---
title: '数据中心激活协调模式: Exchange 2013 Help'
TOCTitle: 数据中心激活协调模式
ms:assetid: 57e4bf22-eeae-42a5-beb3-d68d06489592
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd979790(v=EXCHG.150)
ms:contentKeyID: 50490634
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 数据中心激活协调模式

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2014-07-14_

数据中心激活协调 (DAC) 模式是数据库可用性组 (DAG) 的属性。DAC 模式默认处于禁用状态，但应该为具有两个或更多使用连续复制的成员的所有 DAG 启用该模式。不应为采用第三方复制模式的 DAG 启用 DAC 模式，除非第三方供应商指定这样做。

DAC 模式用于控制 DAG 的启动数据库装入行为。在数据中心故障回复期间，此控件旨在防止数据库级别上出现网络分区。分区（也称为\&quot;分区症\&quot;）是导致正在装入的数据库副本成为同一个 DAG 上两个无法进行通信的成员上的主动副本的症状。分区无法使用 DAC 模式，因为 DAC 模式要求 DAG 成员首先获得装入数据库的权限，然后才能装入数据库。

例如，请考虑一种情况，即主数据中心包含两个 DAG 成员和见证服务器，第二个数据中心包含两个其他 DAG 成员。在这种情况中个，DAG 并不处于 DAC 模式中。因为主数据中心断电了，因此您在第二个数据中心激活 DAG。最终，主数据中心恢复了供电，在断电前已进行了仲裁的主数据中心的 DAG 成员将启动并装入其数据库。因为主数据中心恢复供电时没有通过网络连接到第二个数据中心，而且因为 DAG 并非处于 DAC 模式中，因此 DAG 内的活动数据库出现了分区症。

## DAC 模式的工作原理

DAC 模式包含了数据中心激活协调协议 (DACP)，以此防止出现网络分区。在启用 DAC 模式时，即使 DAG 成员已进行了仲裁，也不会自动装入数据库。相反，DACP 可用于确定 DAG 的当前状态，以及活动管理器是否应尝试装入数据库。

您可能将 DAC 模式视为用于装入数据库的应用程序级别仲裁。若要了解 DACP 的用途以及工作原理，必须了解其旨在处理的主要情况。请考虑双数据中心的情况。假设主数据中心中电源完全中断。在这种情况下，所有服务器和 WAN 都停止运行，所以组织决定激活备用数据中心。在几乎所有这种恢复方案中，当主数据中心恢复通电时，WAN 连接通常不会立即恢复。这意味着主数据中心中的 DAG 成员将通电，但无法与已激活的备用数据中心的 DAG 成员通信。主数据中心应始终包含大部分 DAG 仲裁投票者，这意味着恢复通电后，即使备用数据中心的 DAG 成员未连接 WAN，主数据中心中的 DAG 成员也占大部分，因此拥有仲裁。拥有仲裁后，这些服务器可以装入其数据库，这又会导致与现已装入激活的备用数据中心的实际主动数据库有差异，所以这是个问题。

创建 DACP 就是为了解决此问题。活动管理器在内存中存储一个数位（0 或 1），该数位告诉 DAG 是否允许装入服务器上以活动状态分配的本地数据库。当 DAG 正以 DAC 模式运行时，活动管理器每次启动时，该数位都被设置为 0，表示不允许装入数据库。因为 DAG 处于 DAC 模式，所以服务器必须尝试与其知道的 DAG 的其他所有成员通信，以便获取另一个 DAG 成员，告诉它是否可以装入以活动状态分配给它的本地数据库。答案将以 DAG 中其他活动管理器的数位设置形式提供。如果另一个服务器将其数位设置为 1 进行响应，这意味着服务器允许装入数据库，这样服务器启动时将其数位设置为 1，并装入其数据库。

但是当主数据中心恢复供电时（这时服务器恢复，但 WAN 连接尚未恢复），主数据中心内所有 DAG 成员的 DACP 位值将为 0；因此开始在已恢复的主数据中心内备份的服务器都不会装入数据库，因为它们都无法与 DACP 位值为 1 的 DAG 成员通信。

## 具有两个成员的 DAG 的 DAC 模式

具有两个成员的 DAG 的固有限制会导致仅靠 DACP 位无法完全防止应用程序级网络分区症状。对于仅有两个成员的 DAG，DAC 模式也会使用 DAG 见证服务器的启动时间来确定是否可以在启动时装入数据库。会将见证服务器的启动时间与 DACP 位设置为 1 时的时间进行比较。

  - 如果设置 DACP 位的时间早于见证服务器的启动时间，则系统会假设 DAG 成员和见证服务器同时重新启动（可能是因为主数据中心断电），不允许 DAG 成员装入数据库。

  - 如果设置 DACP 位的时间晚于见证服务器的启动时间，则系统会假设 DAG 成员由于某种其他原因（可能是用于执行维护的计划中断，或可能是与 DAG 成员无关的系统崩溃或断电）而重新启动，允许 DAG 成员装入数据库。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>因为见证服务器的启动时间用于确定 DAG 成员是否可以在启动时装入活动数据库，所以绝不能同时重新启动见证服务器和唯一的 DAG 成员。这样做可能会使 DAG 成员处于无法在启动时装入数据库的状态。如果发生这种情况，则必须在 DAG 上运行 <a href="https://technet.microsoft.com/zh-cn/library/dd351169(v=exchg.150)">Restore-DatabaseAvailabilityGroup</a> cmdlet。这可重置 DACP 位并允许 DAG 成员装入数据库。</td>
</tr>
</tbody>
</table>


## DAC 模式的其他好处

除了在应用程序级防止网络分区症状之外，通过 DAC 模式还可以使用用于执行数据中心切换的内置站点恢复 cmdlet。其中包括：

  - [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd335133\(v=exchg.150\))

  - [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd351169\(v=exchg.150\))

  - [Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd335076\(v=exchg.150\))

为不处于 DAC 模式的 DAG 执行数据中心切换需要结合使用 Exchange 工具和群集管理工具。有关详细信息，请参阅[数据中心切换](datacenter-switchovers-exchange-2013-help.md)。

## 启用 DAC 模式

只能通过使用 Exchange 命令行管理程序启用 DAC 模式。具体来说，您可以使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd297934\(v=exchg.150\)) cmdlet 启用 DAC 模式，如以下示例所示。

    Set-DatabaseAvailabilityGroup -Identity DAG2 -DatacenterActivationMode DagOnly

在前面的示例中，为 DAG2 启用了 DAC 模式。

有关启用 DAC 模式的详细信息，请参阅[配置数据库可用性组属性](configure-database-availability-group-properties-exchange-2013-help.md)和[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd297934\(v=exchg.150\))。

