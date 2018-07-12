---
title: '邮件重试间隔、重新提交间隔和过期间隔: Exchange 2013 Help'
TOCTitle: 邮件重试间隔、重新提交间隔和过期间隔
ms:assetid: 03020e6f-4c01-4c6e-ae47-fd74d4c4f96a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ891103(v=EXCHG.150)
ms:contentKeyID: 51408189
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮件重试间隔、重新提交间隔和过期间隔

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

在 Microsoft Exchange Server 2013 中，传递失败的邮件可能会根据邮件来源和目的地要求重试、重新提交和设置过期期限等。“重试”是重新尝试与目的地建立连接。“重新提交”是将邮件发送回提交队列的操作，以便分类程序重新处理。如果在指定时段内所有传递操作均失败，则邮件“过期”。邮件过期后，发件人会收到传递失败的通知。然后系统会从队列中删除该邮件。

在重试、重新提交或过期这三种情况下，均可以在系统对邮件执行自动操作前手动介入。

有关如何配置这些间隔的说明，请参阅[配置邮件重试间隔、重新提交间隔和过期间隔](configure-message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md)。

## 邮件重试的配置选项

传输服务器无法连接到下一个跃点时，队列的状态将变为“重试”。将继续尝试连接，直到队列过期或已建立连接。

## 自动邮件重试的配置选项

下表中描述了邮件重试间隔可用的配置选项。

### 邮件重试间隔可用的配置选项

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>参数或项名称</th>
<th>默认值</th>
<th>配置位置</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueGlitchRetryCount</em></p></td>
<td><p>4</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>此项指定传输服务器连接目标服务器遇到问题后立即尝试连接的次数。此类连接问题通常是时间非常短的网络中断所致。</p>
<p>此项的有效输入是从 0 到 15 的整数。</p>
<p>通常，除非网络不可靠并且继续出现许多意外断开连接的情况，否则，不必修改此项。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueGlitchRetryInterval</em></p></td>
<td><p><code>00:01:00</code> 或 1 分钟</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>此项控制 <em>QueueGlitchRetryCount</em> 项指定的连接尝试之间的连接间隔。</p>
<p>通常，除非网络不可靠并且继续出现许多意外断开连接的情况，否则，不必修改此参数。</p></td>
</tr>
<tr class="odd">
<td><p><em>TransientFailureRetryCount</em></p></td>
<td><p>6</p></td>
<td><p><strong>Set-TransportService</strong>cmdlet 或 Exchange 管理中心 (EAC) 的服务器属性</p></td>
<td><p>此参数指定 <em>QueueGlitchRetryCount</em> 和 <em>QueueGlitchRetryInterval</em> 项所控制的连接尝试失败后尝试连接的次数。使 <em>QueueGlitchRetryCount</em> 和 <em>QueueGlitchRetryInterval</em> 项失效的连接问题可能是服务器重新启动或缓存 DNS 查找失败之类的事件所致。</p>
<p>此参数的有效输入是从 0 到 15 的整数。如果将此参数设置为 0，则下一次连接尝试由 <em>OutboundConnectionFailureRetryInterval</em> 参数控制。</p></td>
</tr>
<tr class="even">
<td><p><em>TransientFailureRetryInterval</em></p></td>
<td><ul>
<li><p>邮箱服务器上的传输服务：<code>00:05:00</code> 或 5 分钟</p></li>
<li><p>边缘传输服务器：<code>00:01:00</code> 或 10 分钟</p></li>
</ul></td>
<td><p><strong>Set-TransportService</strong>cmdlet 或 EAC 中的服务器属性</p></td>
<td><p>此参数控制 <em>TransientFailureRetryCount</em> 参数指定的连接尝试之间的连接间隔。</p>
<p>若要指定值，请以时间跨度格式 dd.hh:mm:ss 输入值，其中 d = 天，h = 小时，m = 分钟，s = 秒。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundConnectionFailureRetryInterval</em></p></td>
<td><ul>
<li><p>邮箱服务器上的传输服务：<code>00:10:00</code> 或 10 分钟</p></li>
<li><p>边缘传输服务器：<code>00:30:00</code> 或 30 分钟</p></li>
</ul></td>
<td><p><strong>Set-TransportService</strong>cmdlet 或 EAC 中的服务器属性</p></td>
<td><p>此参数指定以前失败的出站连接尝试的重试间隔。以前失败的连接尝试由 <em>TransientFailureRetryCount</em> 和 <em>TransientFailureRetryInterval</em> 参数控制。</p>
<p>若要指定值，请以时间跨度格式 dd.hh:mm:ss 输入值，其中 d = 天，h = 小时，m = 分钟，s = 秒。</p></td>
</tr>
<tr class="even">
<td><p><em>MessageRetryInterval</em></p></td>
<td><p><code>00:15:00</code> 或者 15 分钟</p></td>
<td><p><strong>Set-TransportService</strong> cmdlet</p></td>
<td><p>此参数指定状态为“重试”的各个邮件的重试间隔。建议您不要修改默认值，除非 Microsoft 客户服务和支持人员建议您这样做。</p></td>
</tr>
<tr class="odd">
<td><p><em>MailboxDeliveryQueueRetryInterval</em></p></td>
<td><p><code>00:05:00</code> 或 5 分钟</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>此项指定队列尝试连接无法成功访问的目标邮箱数据库的邮箱传输传递服务的频率。</p>
<p>若要指定值，请以时间跨度格式 dd.hh:mm:ss 输入值，其中 d = 天，h = 小时，m = 分钟，s = 秒。</p>
<p>此项的有效输入范围是 00:00:01 到 1.00:00:00。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 手动邮件重试的配置选项

如果传递队列处于“重试”状态，可以在 Exchange 工具箱中使用队列查看器或在命令行管理程序中使用 **Retry-Queue** cmdlet 手动强制立即尝试连接。手动重试优先于安排的下一次重试时间。如果连接未成功，则重置重试间隔计时器。传递队列必须处于“重试”状态，此操作才能生效。

有关详细信息，请参阅[管理队列](manage-queues-exchange-2013-help.md)中的“重试队列”部分。

返回顶部

## 延迟 DSN 邮件的配置选项

每次发生邮件传递失败之后，边缘传输服务器或邮箱服务器上的传输服务会生成一个延迟发送状态通知 (DSN) 邮件，并将其排入队列以等待传递到未送达邮件的发件人。仅在指定的延迟通知超时间隔后且在该时间内送达邮件失败的情况下，才会发送此延迟 DSN 邮件。默认情况下，延迟通知超时间隔为 4 小时。此延迟可以防止由于临时邮件传输失败而引起发送不必要的延迟 DSN 邮件。可针对源自 Exchange 组织内部或外部的邮件选择性地启用或禁用发送延迟 DSN 通知邮件。

下表描述了延迟 DSN 通知邮件可用的配置选项。

### 延迟 DSN 通知邮件可用的配置选项

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>参数名称</th>
<th>默认值</th>
<th>位置</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code> 4 小时</p></td>
<td><p><strong>Set-TransportService</strong> 或 EAC 中的服务器属性</p></td>
<td><p>此参数指定服务器向发件人发送延迟 DSN 邮件之前的等待时间。此参数的值应始终大于 <em>TransientFailureRetryCount</em> 参数值和 <em>TransientFailureRetryInterval</em> 参数值的乘积。</p>
<p>若要指定值，请以时间跨度格式 dd.hh:mm:ss 输入值，其中 d = 天，h = 小时，m = 分钟，s = 秒。</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>此参数指定延迟 DSN 邮件是否可发送到 Exchange 组织外部的邮件发件人。</p>
<p>此参数的有效输入值为 <code>$true</code> 或 <code>$false</code>。</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>此参数指定延迟 DSN 邮件是否可发送到 Exchange 组织内部的邮件发件人。</p>
<p>此参数的有效输入值为 <code>$true</code> 或 <code>$false</code>。</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 在 Exchange 2007 集线器传输服务器上，所有 <em>ExternalDSN*</em> 和 <em>InternalDSN*</em> 参数能在 <strong>Set-TransportServer</strong> cmdlet 中使用，而不能在 <strong>Set-TransportConfig</strong> cmdlet 中使用。如果组织中有任何 Exchange 2007 集线器传输服务器，则需要在每个 Exchange 2007 集线器传输服务器上使用 <strong>Set-TransportServer</strong> cmdlet 来更改这些值。


返回顶部

## 邮件重新提交的配置选项

重新提交邮件可以将未送达的邮件发送回提交队列，以便分类程序重新进行处理。

## 自动邮件重新提交

如果传递队列处于“重试”状态并且在指定时段内一直无法成功地传递任何邮件，则将自动重新提交未送达的邮件。该时间由 EdgeTransport.exe.config 应用程序配置文件中的 *MaxIdleTimeBeforeResubmit* 项控制。只有传递队列中的邮件可以进行自动重新提交。

若要指定值，请以时间跨度格式 dd.hh:mm:ss 输入值，其中 d = 天，h = 小时，m = 分钟，s = 秒。

默认值为 `12:00:00` 或 12 小时。

## 手动邮件重新提交

可以在邮箱服务器或边缘传输服务器上的传输服务中手动重新提交具有以下状态的邮件：

  - 处于重试状态的传递队列。队列中的邮件不得处于“挂起”状态。

  - 无法到达队列中未处于“挂起”状态的邮件。

  - 病毒邮件队列中的邮件。

有关病毒邮件队列和无法到达队列的详细信息，请参阅本主题[队列](queues-exchange-2013-help.md)中的“关于病毒邮件队列和无法到达队列”。

如果希望手动重新提交传递队列或无法到达队列中的邮件，而不是等待 *MaxIdleTimeBeforeResubmit* 参数指定的时间，则必须使用包含 *Resubmit* 参数的 **Retry-Queue** cmdlet。若要手动重新提交病毒邮件队列中的邮件，可以使用队列查看器或 **Resume-Message** cmdlet 恢复邮件。有关详细信息，请参阅[管理队列](manage-queues-exchange-2013-help.md)中的“重新提交队列中的邮件”部分。

手动重新提交邮件可以使用的另一种方式是挂起邮件，将邮件导出到文件扩展名为 .eml 的文本文件，然后将 .eml 文件复制到任何邮箱服务器或边缘传输服务器上的重播目录。这种重新提交方法适用于传递队列或无法到达队列中的邮件。病毒邮件队列中的邮件已处于“挂起”状态。提交队列中的邮件不得挂起或导出。

> [!NOTE]  
> 从队列中导出邮件时，不会将邮件从队列中删除。导出邮件并使用重播目录成功地重新提交这些邮件后，应删除挂起的邮件，以防重复提交邮件。


有关详细信息，请参阅[从队列导出邮件](export-messages-from-queues-exchange-2013-help.md)。

返回顶部

## 邮件过期的配置选项

“邮件过期超时间隔”指定边缘传输服务器或邮箱服务器上的传输服务尝试传递失败邮件的最长时间。如果无法在过期超时间隔结束之前成功传递邮件，则会将一个包含原始邮件或邮件头的 NDR 传递给发件人。

## 自动邮件过期

邮件过期超时间隔由 **Set-TransportService** cmdlet 中或 EAC 中的服务器属性中的 *MessageExpirationTimeOut* 参数控制。

若要指定值，请以时间跨度格式 dd.hh:mm:ss 输入值，其中 d = 天，h = 小时，m = 分钟，s = 秒。

默认值为 `2.00:00:00` 或 2 天。此参数的有效输入范围为 `00:00:05` 到 `90.00:00:00`。

## 手动邮件过期

尽管无法手动强制邮件过期，但是可以手动删除除了提交队列之外的任何其他队列中的邮件，可以发送或不发送 NDR。

有关详细信息，请参阅[管理队列中的邮件](manage-messages-in-queues-exchange-2013-help.md)中的“从队列中删除邮件”部分。

返回顶部

