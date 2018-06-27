---
title: '排队优先级: Exchange 2013 Help'
TOCTitle: 排队优先级
ms:assetid: 6edbd826-fe55-435b-9c63-48e6365c3d09
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb691107(v=EXCHG.150)
ms:contentKeyID: 51408233
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 排队优先级

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

*排队优先级*是 Microsoft Exchange Server 2013 的一项功能，该功能使发件人定义的邮件优先级能够影响邮箱服务器上传输服务对邮件的处理。

发件人在创建和发送邮件时，会在 Microsoft Outlook 中分配邮件优先级。发件人可以在 Outlook 中设置下列任一邮件优先级值：

  - 低重要性

  - 普通重要性

  - 高重要性

在 Outlook 或 Outlook Web App 中创建的邮件的默认优先级是普通优先级。邮件优先级存储在邮件头的 `X-Priority` 头字段中。

在 Exchange 2013 组织中发送或接收的每封邮件都必须由邮箱服务器上的传输服务进行分类，然后才能路由和传递该邮件。邮箱服务器上传输服务中的分类程序从提交队列中一次拣选一封邮件，并对邮件执行收件人解析、路由解析和内容转换，然后再将该邮件放入传递队列。有关详细信息，请参阅[邮件流](mail-flow-exchange-2013-help.md)。

传递队列基于邮件目标动态创建。有关详细信息，请参阅[队列](queues-exchange-2013-help.md)。

目标相同的所有邮件将放入同一个传递队列。排队优先级将影响邮件从传递队列向目标邮件服务器的传输。启用排队优先级后，高优先级邮件将先于普通优先级邮件传送到目标，而普通优先级邮件将先于低优先级邮件传送到目标。基于邮件优先级确定邮件传递优先级，有助于为邮件传递时间定义具体的服务级别协议 (SLA) 要求。

## 配置排队优先级的选项

对排队优先级的支持由 `%ExchangeInstallPath%bin\EdgeTransport.exe.config` XML 应用程序配置文件中的键进行控制。有关如何配置排队优先级的说明，请参阅[启用和配置队列优先级](enable-and-configure-priority-queuing-exchange-2013-help.md)。

下表对每个键进行了详细的说明。

### EdgeTransport.exe.config 文件中的排队优先级键

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>键</th>
<th>默认值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>PriorityQueuingEnabled</em></p></td>
<td><p><code>false</code></p></td>
<td><p>此键可以在邮箱服务器上的传输服务中启用或禁用排队优先级。此键的有效输入值为 <code>true</code> 或 <code>false</code>。</p>
<p>当此键为 <code>false</code> 时，排队优先级会被禁用，并且忽略 EdgeTransport.exe.config 文件中的所有排队优先级邮件限制。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxHighPriorityMessageSize</em></p></td>
<td><p><code>250KB</code></p></td>
<td><p>此键可以指定高优先级邮件允许的最大大小。如果高优先级邮件大于此键指定的值，该邮件将自动从高优先级降级为普通优先级。</p>
<p>此键的值应当明显小于 <strong>Set-TransportConfig</strong> cmdlet 上 <em>MaxSendMessageSize</em> 参数的值。此参数的默认值是 <code>10 MB</code>。这两个值之间的差异有助于确保高优先级邮件的传递时间一致并且可预测。</p>
<p>输入值时，请用下列单位之一限定该值：</p>
<ul>
<li><p>KB（千字节）</p></li>
<li><p>MB（兆字节）</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>LowPriorityDelayNotificationTimeout</em></p>
<p><em>NormalPriorityDelayNotificationTimeout</em></p>
<p><em>HighPriorityDelayNotificationTimeout</em></p></td>
<td><p><strong>低</strong> <code>8:00:00</code>（8 小时）</p>
<p><strong>正常</strong> <code>4:00:00</code>（4 小时）</p>
<p><strong>高</strong> <code>00:30:00</code>（30 分钟）</p></td>
<td><p>这些键可以根据邮件优先级指定延迟发送状态通知 (DSN) 邮件的超时间隔。</p>
<p>每次邮件发送失败之后，传输服务器会生成一个延迟 DSN 邮件，并将其排入队列，以等待发送至未送达邮件的发件人。仅在指定的延迟通知超时间隔后且在该时间内送达邮件失败的情况下，才会发送此延迟 DSN 邮件。此延迟可以防止由于临时邮件传输失败而引起发送不必要的延迟 DSN 邮件。</p>
<p>若要指定值，请以时间跨度格式 dd.hh:mm:ss 输入值，其中 d = 天，h = 小时，m = 分钟，s = 秒。</p></td>
</tr>
<tr class="even">
<td><p><em>LowPriorityMessageExpirationTimeout</em></p>
<p><em>NormalPriorityMessageExpirationTimeout</em></p>
<p><em>HighPriorityMessageExpirationTimeout</em></p></td>
<td><p><strong>低</strong> <code>2.00:00:00</code>（2 天）</p>
<p><strong>正常</strong> <code>2.00:00:00</code>（2 天）</p>
<p><strong>高</strong> <code>8:00:00</code>（8 小时）</p></td>
<td><p>这些键可以指定传输服务尝试发送失败邮件的最长时间。如果无法在过期超时间隔结束之前成功传递邮件，则会将一个包含原始邮件或邮件头的未送达报告 (NDR) 传递给发件人。</p>
<p>若要指定值，请以时间跨度格式 dd.hh:mm:ss 输入值，其中 d = 天，h = 小时，m = 分钟，s = 秒。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxPerDomainLowPriorityConnections</em></p>
<p><em>MaxPerDomainNormalPriorityConnections</em></p>
<p><em>MaxPerDomainHighPriorityConnections</em></p></td>
<td><p><strong>低</strong>   2</p>
<p><strong>正常</strong>   15</p>
<p><strong>高</strong>   3</p></td>
<td><p>这些键可以指定传输服务与任一单个远程域可以建立的最大连接数。使用邮箱服务器上的传递队列和发送连接器建立传出到远程域的连接。</p>
<p>这三个键的总值应当小于或等于 <strong>Set-TransportService</strong> cmdlet 上 <em>MaxPerDomainOutboundConnections</em> 参数的值。此参数的默认值是 <code>20</code>。</p></td>
</tr>
</tbody>
</table>


## 排队优先级如何影响邮箱服务器上的其他邮件限制

经过传输服务的所有邮件受各种邮件重试限制、重新提交限制和过期限制的约束。有关详细信息，请参阅[邮件大小限制](message-size-limits-exchange-2013-help.md)。

**Set-TransportService** cmdlet 中可用的某些邮件限制在 EdgeTransport.exe.config 应用程序配置文件中有对应的排队优先级邮件限制。下表说明这些对应的邮件限制。

### Set-TransportService cmdlet 中与 EdgeTransport.exe.config 中的排队优先级邮件限制对应的邮件限制

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>来源</th>
<th>参数或键</th>
<th>默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code>（4 小时）</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityDelayNotificationTimeout</em></p></td>
<td><p><code>4:00:00</code>（4 小时）</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MessageExpirationTimeOut</em></p></td>
<td><p><code>2.00:00:00</code>（2 天）</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityMessageExpirationTimeout</em></p></td>
<td><p><code>2.00:00:00</code>（2 天）</p></td>
</tr>
</tbody>
</table>


禁用排队优先级时，将忽略 EdgeTransport.exe.config 配置文件中的所有排队优先级邮件限制。**Set-TransportService** cmdlet 中的所有邮件限制适用于经过邮箱服务器上传输服务的所有邮件。

启用排队优先级时，EdgeTransport.exe.config 配置文件中的排队优先级邮件限制将覆盖 **Set-TransportService** cmdlet 中对应的邮件限制。**Set-TransportService** cmdlet 中的其他所有邮件限制仍适用于经过邮箱服务器上传输服务的低优先级、普通优先级和高优先级邮件。

## 排队优先级的用户设置

**Set-Mailbox** cmdlet 包含 *DowngradeHighPriorityMessagesEnabled* 参数。默认值为 `$false`。此参数设置为 `$true` 时，从该邮箱发送的任何高优先级邮件将自动降级为普通优先级。

