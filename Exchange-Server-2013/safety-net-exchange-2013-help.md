---
title: 'Safety Net: Exchange 2013 Help'
TOCTitle: Safety Net
ms:assetid: d0abb807-3b12-4c7d-bc7e-769b87c84ccb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657495(v=EXCHG.150)
ms:contentKeyID: 50491595
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Safety Net

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

在 Microsoft Exchange Server 2013 中，邮箱高可用性的主要机制为数据库可用性组 (DAG)。有关 DAG 的详细信息，请参见[管理数据库可用性组](managing-database-availability-groups-exchange-2013-help.md)。“传输转储程序”最先在 Exchange 2007 中引入，并在 Exchange 2010 中得到进一步改善，以便在邮件成功提供给 DAG 中的邮箱后，提供冗余的邮件副本。在 Exchange 2010 中，传输转储程序通过维持尚未复制到 DAG 中被动邮箱数据库副本的一队成功交付的邮件，帮助防止数据丢失。如果邮箱数据库或服务器故障需要创建邮箱数据库的过期副本，则会自动将传输转储程序中的邮件重新传递至邮箱数据库新的活动副本。

传输转储程序已在 Exchange 2013 中得到改进，并且现在称为“Safety Net”。

在此将描述 Safety Net 与 Exchange 2010 中的传输转储程序如何相似：

  - Safety Net 是一个队列，与邮箱服务器上的传输服务相关。该队列存储由服务器成功处理的邮件副本。

  - 您可指定在成功处理的邮件到期并被自动删除前，Safety Net 将把这些邮件保存多长时间。默认为 2 天。

这里将讨论 Safety Net 在 Exchange 2013 中有何不同：

  - Safety Net 不需要 DAG。对于不属于 DAG 的邮箱服务器，Safety Net 在本地 Active Directory 站点中的其他邮箱服务器上存储传递的邮件的副本。

  - 现在 Safety Net 本身是冗余的，并且不再是单点故障。这引入了“Primary Safety Net”和“Shadow Safety Net”概念。如果 Primary Safety Net 在 12 个小时以上的时间内不可用，则重新提交成为卷影重新提交请求的请求，并且会从 Shadow Safety Net 重新提交邮件。

  - Safety Net 会负责 DAG 环境中一些卷影冗余的工作。卷影冗余在等待传递的邮件复制到 DAG 中其他邮箱服务器上的邮箱数据的被动副本之前，无需在卷影队列中保留传递的邮件的其他副本。传递的邮件的副本已存储在 Safety Net 中，因此如果需要，可从 Safety Net 重新提交邮件。

  - 在 Exchange 2013 中，传输高可用性不仅仅邮件冗余的最大努力。Exchange 2013 尝试确保邮件冗余。因此，您不能指定 Safety Net 的最大大小限制。您可指定在成功删除邮件前，Safety Net 将把这些邮件保存多长时间。

**目录**

Safety Net 工作方式

从 Safety Net 重新提交邮件

从 Shadow Safety Net 重新提交邮件

## Safety Net 工作方式

卷影冗余会在传输邮件时保留邮件的冗余副本。在成功处理邮件后，Safety Net 会保留邮件的冗余副本。因此，Safety Net 会在卷影冗余结束处开始。关于卷影冗余的相同概念，包括传输高可用性界限、主要邮件、主要服务器、卷影邮件和卷影服务器也适用于 Safety Net。有关详细信息，请参阅[卷影冗余](shadow-redundancy-exchange-2013-help.md)。

Primary Safety Net 在传输服务成功处理邮件之前，存在于保留主要邮件的邮箱服务器上。这可能意味着邮件被传递到目标邮箱服务器上的邮箱传输服务。或者，可通过指定为通往目标 DAG 或 Active Directory 站点上集线器站点的 Active Directory 站点中的邮箱服务器中继邮件。在主要服务器处理主要邮件之后，会将邮件从活动队列移动到同一服务器上的 Primary Safety Net。

Shadow Safety Net 存在于保留卷影邮件的邮箱服务器上。在卷影服务器确定主要服务器已成功处理主要邮件后，卷影服务器将卷影邮件从卷影队列移动至同一服务器上的 Shadow Safety Net 中。尽管看上去很明显，Shadow Safety Net 的存在需要启用卷影冗余，并且在 Exchange 2013 中默认启用卷影冗余。

在下表中描述了 Safety Net 使用的参数。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>默认值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportConfig</strong> 上的 <em>SafetyNetHoldTime</em></p></td>
<td><p>2 天</p></td>
<td><p>成功处理主要邮件的时间长度存储在 Primary Safety Net 中，而确认的卷影邮件存储在 Shadow Safety Net 中。</p>
<p>您也可在 Exchange 管理中心 (EAC) 中指定该值，路径为“邮件流”&gt;“接收连接器”&gt;“更多选项”<img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="更多选项图标" alt="更多选项图标" />&gt;“组织传输设置”&gt;“Safety Net”&gt;“Safety Net 保留时间”。</p>
<p>在 <strong>Set-TransportService</strong> 上的 <em>SafetyNetHoldTime</em> 和 <em>MessageExpirationTimeout</em> 求和之后，未确认的卷影邮件最终过期。</p>
<p>为了避免 Safety Net 重新提交期间数据丢失，<em>SafetyNetHoldTime</em> 的值必须大于或等于邮箱数据库滞后副本的 <strong>Set-MailboxDatabaseCopy</strong> 上的 <em>ReplayLagTime</em> 的值。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailboxDatabaseCopy</strong> 上的 <em>ReplayLagTime</em></p></td>
<td><p>未配置</p></td>
<td><p>Microsoft Exchange 复制服务在重播被复制到被动数据库副本的日志文件之前应等待的时间。将此参数设置为大于 0 的值将创建滞后邮箱数据库副本。最大值为 14 天。</p>
<p>为了避免 Safety Net 重新提交期间数据丢失，<em>ReplayLagTime</em> 的值必须小于或等于邮箱数据库滞后副本的 <strong>Set-TransportConfig</strong> 上的 <em>SafetyNetHoldTime</em> 的值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong> 上的 <em>MessageExpirationTimeout</em></p></td>
<td><p>2 天</p></td>
<td><p>邮件在到期之前可以保留在队列中多长时间。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportConfig</strong> 上的 <em>ShadowRedundancyEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> 启用组织中的所有传输服务器的卷影冗余。</p></li>
<li><p><code>$false</code> 禁用组织中的所有传输服务器的卷影冗余。</p></li>
</ul>
<p>冗余的 Safety Net 需要启用卷影冗余。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 从 Safety Net 重新提交邮件

从 Safety Net 重新提交邮件通过管理 DAG 和邮箱数据库副本的 Microsoft Exchange 复制服务的活动管理器组件启动。从 Safety Net 重新提交邮件无需手动操作。有关 Active Manager 的详细信息，请参阅[活动管理器](active-manager-exchange-2013-help.md)。

有两种基本 Safety Net 邮件重新提交情景：

  - 在 DAG 中进行邮箱数据库的自动或手动故障转移后。

  - 在激活邮箱数据库的滞后副本后。

“滞后邮箱数据库副本”或“滞后副本”是邮箱数据库的被动副本，在其中会有意延迟对数据库的更新，以防止在逻辑上破坏邮箱数据库。有关详细信息，请参阅[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)。

两个场景之间的唯一明显区别在于要倒退多少时间来从 Safety Net 重新提交邮件。通常，对于 DAG 中的故障转移，邮箱数据库的新活动副本通常落后于旧的活动副本数分钟到数小时。邮箱数据库的滞后副本通常落后于旧活动副本数天。

从 Safety Net 成功重新提交滞后副本的主要要求是邮件存储在 Safety Net 中的时间必须大于或等于邮箱数据库滞后副本的滞后时间。换句话讲，对于滞后副本，**Set-TransportConfig** 上 *SafetyNetHoldTime* 的值必须大于或等于 **Set-MailboxDatabaseCopy** 上 *ReplayLagTime* 的值。

返回顶部

## 从 Shadow Safety Net 重新提交邮件

与从 Primary Safety Net 重新提交邮件相似，从 Shadow Safety Net 重新提交邮件是完全自动进行，并且无需手动干预。

如果活动管理器请求在特定时段从 Safety Net 重新提交邮件，请求将转至邮箱服务器上的传输服务，其中 Primary Safety Net 会保留所需时段的邮件副本。在大型 Exchange 组织中，所需的邮件很可能存在于多个邮箱服务器上的 Safety Net 中，尤其是在所需时段较长时。

如果不进行优化，从 Safety Net 重新提交邮件可能潜在导致大量重复传递。在 Exchange 组织中重复传递并非问题，因为重复邮件检测功能可防止用户看到重复的邮件副本。但是对于 Exchange 组织外的收件人的重复邮件传递将导致重复的邮件副本。幸运的是，在 Exchange 2013 中对从 Safety Net 重新提交邮件进行了优化，以减少重复邮件传递。

如果 Primary Safety Net 最初没有响应，或在邮件重新提交期间变得没响应，在放弃之前的 12 小时内，活动管理器将继续尝试与其联系。在 12 小时后，会在传输高可用性限制内向所有邮箱服务器上的传输服务发送广播，请求对所需邮箱数据库在所需时段内从 Safety Net 重新提交邮件。如果 Shadow Safety Net 响应，则只在所需时段内对所需邮箱数据库重新提交邮件。

对于存储于 Shadow Safety Net 中的卷影邮件，有两个重要的注意事项：

  - Shadow Safety Net 不知道主要服务器在何处传输主要邮件。

  - Shadow Safety Net 中的卷影邮件仅包含原始邮件信封收件人，而不是向其传递主要邮件的实际收件人。例如，邮件信封收件人可能是需要扩展的通讯组。

  - Shadow Safety Net 中的邮件没有任何在主要服务器处理邮件后发生的邮件更新。例如，邮件编码或内容转换。

从 Shadow Safety Net 重新提交的卷影邮件需要通过邮箱服务器上的传输服务完整分类和处理。就邮箱服务器资源方面而言，从 Shadow Safety Net 重新提交大量卷影邮件可能开销巨大。幸运的是，也对从 Shadow Safety Net 重新提交卷影邮件进行了优化，从而只对请求时段和请求邮箱数据库的 Shadow Safety Net 中的邮件进行重新提交。

在以下场景中，对邮件重新提交期间 Primary Safety Net 和 Shadow Safety Net 之间的交互进行了说明。

1.  活动管理器请求对时段 5:00 到 9:00 对邮箱数据库从 Safety Net 重新提交邮件。但是，由于硬件故障，拥有 Primary Safety Net 的邮箱服务器发生崩溃。活动管理器会在 12 小时内重复尝试联系 Primary Safety Net。

2.  在 12 小时后，活动管理器会在传输高可用性界限内向所有邮箱服务器上的传输服务发送广播邮件，寻找时间段 5:00 至 9:00 之间包含目标邮箱数据库邮件的其他 Safety Net。Shadow Safety Net 会做出响应，对时段 5:00 至 9:00 重新提交邮箱数据库的邮件。

如果 Primary Safety Net 在部分请求的提交间隔期间脱机，则会发生有趣的交互，如下面的情景中所述。

1.  拥有 Primary Safety Net 的邮箱服务器上的队列数据库损坏，并在 7:00 新建了队列数据库。从 1:00 到 7:00，存储在 Primary Safety Net 中的所有主要邮件都会丢失，但是服务器能够存储从 7:00 开始在 Safety Net 中成功传递的邮件的副本。

2.  活动管理器请求对时间段 1:00 到 9:00 对邮箱数据库从 Safety Net 重新提交邮件。

3.  Primary Safety Net 对时间段 7:00 到 9:00 重新提交邮件。

4.  Primary Safety Net 会在传输高可用性界限内向所有邮箱服务器上的传输服务发送广播邮件，寻找时间段 1:00 至 7:00 之间（在该时段 Primary Safety Net 没有邮件）包含目标邮箱数据库邮件的其他 Safety Net。Shadow Safety Net 代表 Primary Safety Net 生成第二次重新提交请求，对时间段 1:00 到 7:00 对目标邮箱数据库重新提交卷影邮件。

在从 Safety Net 重新提交邮件时，有一些需要考虑的其他问题。

1.  禁止所有传递状态通知 (DSN) 以及非传递报告 (NDR) 以进行 Safety Net 重新提交。例如，如果主要邮件导致 NDR，则不会传递重新提交的邮件的 NDR。

2.  当 Shadow Safety Net 重新提交邮件时，从通讯组删除的用户可能不会收到重新提交的邮件。例如，邮件被发送给包含用户 A 和用户 B 的组，同时这两个收件人都可收到邮件。随后从组中删除用户 B。稍后，将会对拥有用户 B 的邮箱的邮箱数据库发出从 Primary Safety Net 进行重新提交的请求。但是 Primary Safety Net 会在 12 小时以上的时间内不可用，因此 Shadow Safety Net 服务器会响应并重新提交受影响邮件。在扩展了通讯组的重新提交期间，用户 B 并非通讯组的成员，并且不会收到重新提交的邮件的副本。

3.  当 Shadow Safety Net 重新提交邮件时，添加至通讯组的新用户可能会收到旧的重新提交的邮件。例如，邮件被发送给包含用户 A 和用户 B 的组，同时这两个收件人都可收到邮件。用户 C 随后会添加到组中。稍后，将会对拥有用户 C 的邮箱的邮箱数据库发出从 Primary Safety Net 进行重新提交的请求。但是 Primary Safety Net 服务器会在 12 小时以上的时间内不可用，因此 Shadow Safety Net 服务器会响应并重新提交受影响邮件。在扩展了通讯组的重新提交期间，用户 C 是通讯组的成员，并且会收到重新提交的邮件的副本。

返回顶部

