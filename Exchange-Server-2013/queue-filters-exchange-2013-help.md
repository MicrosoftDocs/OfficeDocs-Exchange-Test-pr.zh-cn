---
title: '队列筛选器: Exchange 2013 Help'
TOCTitle: 队列筛选器
ms:assetid: fbfbdcab-e0d2-4ed9-8f7f-e5fa2c87360d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125237(v=EXCHG.150)
ms:contentKeyID: 50492039
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 队列筛选器

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

筛选将生成不同的队列视图。使用队列属性作为筛选器选项。通过指定筛选条件，可以快速找到队列并对队列执行操作。以下方案是如何使用队列筛选管理邮件流的一些示例：

  - 您从 Microsoft System Center Operations Manager 收到表示队列长度已超过设置的阈值的邮件。您希望调查是否存在服务器范围的邮件流问题。
    
    可以通过创建筛选器，查看邮件数超过您认为的正常数目的所有队列。如果表明存在邮件流问题，则可以在继续调查的同时，选中筛选结果中的所有队列并挂起这些队列。

  - 通过挂起多个队列来调查邮件流问题的原因。已确定问题原因是连接器配置不正确，现已得到解决。
    
    可以通过创建筛选器，查看状态为\&quot;已挂起\&quot;的所有队列，然后选中筛选结果中的所有队列并恢复这些队列。

## 筛选队列时要使用的队列属性

可以使用队列属性创建筛选器，找到符合指定条件的队列。可以在队列查看器中创建筛选器，也可以使用队列管理 cmdlet 上的 *Filter* 参数创建筛选器。请注意，队列管理 cmdlet 支持的可筛选属性多于队列查看器。下表列出了筛选可以依据的队列属性以及这些属性的有效值。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>队列查看器队列属性</th>
<th>命令行管理程序队列属性</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>不适用</p></td>
<td><p><code>DeferredMessageCount</code></p></td>
<td><p>此属性标识因收件人解析过程遇到的暂时性错误而返回到提交队列的邮件数量。有关推迟邮件的详细信息，请参阅<a href="recipient-resolution-exchange-2013-help.md">收件人解析</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>传递类型</strong></p></td>
<td><p><code>DeliveryType</code></p></td>
<td><p><strong>DeliveryType</strong> 的有效值在 <a href="queues-exchange-2013-help.md">队列</a> 主题的&amp;quot;NextHopSolutionKey&amp;quot;部分进行了说明。</p></td>
</tr>
<tr class="odd">
<td><p>不适用</p></td>
<td><p><code>Identity</code></p></td>
<td><p>此属性为 <em>&lt;Server&gt;\&lt;Queue&gt;</em> 形式的队列标识。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;队列标识&amp;quot;部分。</p></td>
</tr>
<tr class="even">
<td><p>不适用</p></td>
<td><p><code>IncomingRate</code></p></td>
<td><p>此属性是一个计算的数字，表示邮件进入队列的速度。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;IncomingRate、OutgoingRate 和速度&amp;quot;部分。</p></td>
</tr>
<tr class="odd">
<td><p><strong>上一错误</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>此属性表示队列记录的上一个错误的文本字符串。</p></td>
</tr>
<tr class="even">
<td><p><strong>上次重试时间</strong></p></td>
<td><p><code>LastRetryTime</code></p></td>
<td><p>此属性表示状态为 <code>Retry</code> 的队列上次尝试连接的日期/时间。</p></td>
</tr>
<tr class="odd">
<td><p>不适用</p></td>
<td><p><code>LockedMessageCount</code></p></td>
<td><p>此属性保留供 Microsoft 内部使用，不在内部部署 Exchange 2013 组织中使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>邮件计数</strong></p></td>
<td><p><code>MessageCount</code></p></td>
<td><p>此属性表示该队列中的邮件数。</p></td>
</tr>
<tr class="odd">
<td><p>不适用</p></td>
<td><p><code>NextHopCategory</code></p></td>
<td><p>此属性将队列的下一跃点指定为 <code>Internal</code> 或 <code>External</code>，基于队列的 <strong>DeliveryType</strong> 属性值。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;NextHopSolutionKey&amp;quot;部分。</p></td>
</tr>
<tr class="even">
<td><p>不适用</p></td>
<td><p><code>NextHopConnector</code></p></td>
<td><p>此属性是下一跃点的 GUID，基于队列的 <strong>DeliveryType</strong> 属性值。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;NextHopSolutionKey&amp;quot;部分。</p></td>
</tr>
<tr class="odd">
<td><p><strong>下一跃点域</strong></p></td>
<td><p><code>NextHopDomain</code></p></td>
<td><p>此属性是下一跃点的名称，基于队列的 <strong>DeliveryType</strong> 属性值。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;NextHopSolutionKey&amp;quot;部分。</p></td>
</tr>
<tr class="even">
<td><p><strong>下次重试时间</strong></p></td>
<td><p><code>NextRetryTime</code></p></td>
<td><p>此属性表示状态为 <code>Retry</code> 的队列下一次尝试连接的日期/时间。</p></td>
</tr>
<tr class="odd">
<td><p>不适用</p></td>
<td><p><code>OutgoingRate</code></p></td>
<td><p>此属性是一个计算的数字，表示邮件离开队列的速度。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;IncomingRate、OutgoingRate 和速度&amp;quot;部分。</p></td>
</tr>
<tr class="even">
<td><p>不适用</p></td>
<td><p><code>RiskLevel</code></p></td>
<td><p>此属性保留供 Microsoft 内部使用，不在内部部署 Exchange 2013 组织中使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>状态</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>此属性表示当前的队列状态。队列可为下列状态值之一：&amp;quot;活动&amp;quot;、&amp;quot;正在连接&amp;quot;、&amp;quot;无&amp;quot;、&amp;quot;已挂起&amp;quot;、&amp;quot;就绪&amp;quot;或&amp;quot;重试&amp;quot;。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;队列状态&amp;quot;部分。</p></td>
</tr>
<tr class="even">
<td><p>不适用</p></td>
<td><p><code>TlsDomain</code></p></td>
<td><p>此属性包含目的域的 FQDN（如果已为域安全配置了域）。</p></td>
</tr>
<tr class="odd">
<td><p>不适用</p></td>
<td><p><code>Velocity</code></p></td>
<td><p>此属性包含一个计算的数字，表示队列如何有效处理完毕。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;IncomingRate、OutgoingRate 和速度&amp;quot;部分。</p></td>
</tr>
</tbody>
</table>

