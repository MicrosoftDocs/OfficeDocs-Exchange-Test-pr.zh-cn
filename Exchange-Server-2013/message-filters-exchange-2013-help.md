---
title: '邮件筛选器: Exchange 2013 Help'
TOCTitle: 邮件筛选器
ms:assetid: 8e6187c1-76f0-49da-bc24-2ab57cfb3c2c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123714(v=EXCHG.150)
ms:contentKeyID: 50491013
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 邮件筛选器

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

筛选会在队列中生成不同的邮件视图。通过指定筛选条件，可以迅速找到邮件并对其执行操作。将一封电子邮件发送给多个收件人时，此邮件可能会位于多个队列中。按邮件属性进行筛选时，可跨所有队列查找邮件。以下方案是如何使用邮件筛选管理邮件流的一些示例：

  - 从 Internet 接收电子邮件的邮箱服务器或边缘传输服务器上的提交队列中有大量排队等待传递的邮件。其中很多邮件具有相同的主题。因此你会怀疑有人正在向组织发送垃圾邮件。可以创建一个筛选器来查看所有符合该主题条件的邮件。如果确定这些邮件为垃圾邮件，则可将其全部选中然后将其从传递队列中删除，而不必发送 NDR。

  - 用户报告邮件流缓慢。对队列进行检查，发现很多具有随机主题的邮件似乎来自单个域。可以创建一个筛选器来查看所有来自该域的已进入队列的邮件。如果确定这些邮件为垃圾邮件，则可将其全部选中然后将其从队列中删除，而不必发送 NDR。

## 作为筛选器的邮件属性

可使用邮件属性创建筛选器并查找符合特定条件的邮件。你可以在队列查看器中创建筛选器，也可以使用邮件管理 cmdlet 中的 *Filter* 参数创建筛选器。请注意，邮件管理 cmdlet 支持的可筛选属性数量多于队列查看器。下表列出了可以进行筛选的邮件属性以及与这些属性关联的值。

### 筛选邮件时使用的邮件属性

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>队列查看器邮件属性</th>
<th>命令行管理程序邮件属性</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>接收日期</strong></p></td>
<td><p><code>DateReceived</code></p></td>
<td><p>邮件进入队列时的日期/时间</p></td>
</tr>
<tr class="even">
<td><p>无</p></td>
<td><p><code>DeferReason</code></p></td>
<td><p>此属性标识邮件延迟的原因。如果邮件未延迟，则此属性的值为 <code>None</code>。由于收件人解析过程中遇到暂时错误，延迟的邮件返回到提交队列。有关延迟的邮件的详细信息，请参阅<a href="recipient-resolution-exchange-2013-help.md">收件人解析</a>。可能的值是：</p>
<p><code>AD Transient Failure During Content Conversion</code></p>
<p><code>AD Transient Failure During Resolve</code></p>
<p><code>Agent</code></p>
<p><code>Ambiguous Recipient</code></p>
<p><code>Loop Detected</code></p>
<p><code>Marked As Retry Delivery If Rejected</code></p>
<p><code>Rerouted By Store Driver</code></p>
<p><code>Storage Transient Failure During Content Conversion</code></p>
<p><code>Transient Failure</code></p>
<p><code>Target Site Inbound Mail Disabled</code></p>
<p><code>Recipient Thread Limit Exceeded</code></p>
<p><code>Transient Attribution Failure</code></p>
<p><code>Transient Accepted Domains Load Failure</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>过期时间</strong></p></td>
<td><p><code>ExpirationTime</code></p></td>
<td><p>此属性包含当邮件无法传递而过期并从队列中删除时的日期/时间。</p></td>
</tr>
<tr class="even">
<td><p><strong>发件人地址</strong></p></td>
<td><p><code>FromAddress</code></p></td>
<td><p>此属性包含发件人的 SMTP 地址。</p></td>
</tr>
<tr class="odd">
<td><p>无</p></td>
<td><p><code>Identity</code></p></td>
<td><p>此属性是 <em>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</em> 形式的邮件标识。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;邮件标识&amp;quot;部分。</p></td>
</tr>
<tr class="even">
<td><p><strong>Internet 邮件 ID</strong></p></td>
<td><p><code>InternetMessageId</code></p></td>
<td><p>此属性包含位于邮件头中的 <code>Message-ID:</code> 标头字段的值。该值表示为包含发送 SMTP 服务器的 GUID 和 FQDN 的电子邮件地址。例如：</p>
<p><code>&lt;67D754D6103DC4FB3BA6BC7205DACABA61231@mailbox01.contoso.com&gt;</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>上一错误</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>此属性包含为邮件记录的上一错误的文本。例如，<code>A matching connector cannot be found to route the external recipient</code>。</p></td>
</tr>
<tr class="even">
<td><p>无</p></td>
<td><p><code>MessageLatency</code></p></td>
<td><p>此属性包含当邮件第一次进入服务器的提交队列时与邮件放入队列时之间经过的时间量。该值使用语法 <em>hh:mm:ss.ff</em>，其中 <em>hh</em> 为小时，<em>mm</em> 为分钟，<em>ss</em> 为秒，<em>ff</em> 为秒的分数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>邮件源名称</strong></p></td>
<td><p><code>MessageSourceName</code></p></td>
<td><p>此属性包含一个文本字符串，该字符串指示将邮件提交到队列的传输组件的名称。例如，如果邮件是通过接收连接器传入的，则该值为：<code>SMTP:</code><em>&lt;ConnectorName&gt;</em>。如果邮件是传递状态通知 (DSN)，则该值为 <code>DSN</code>。</p></td>
</tr>
<tr class="even">
<td><p>无</p></td>
<td><p><code>Priority</code></p></td>
<td><p>此属性包含用户在 Outlook 或 Outlook Web App 中分配的邮件优先级。可能的值为 <code>Low</code>、<code>Normal</code> 和 <code>High</code>。有关详细信息，请参阅<a href="priority-queuing-exchange-2013-help.md">排队优先级</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>队列 ID</strong></p></td>
<td><p><code>Queue</code></p></td>
<td><p>此属性是存放邮件的队列的标识。队列标识使用语法 <em>&lt;Server&gt;\&lt;Queue&gt;</em>。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;队列标识&amp;quot;部分。</p></td>
</tr>
<tr class="even">
<td><p>无</p></td>
<td><p><code>RetryCount</code></p></td>
<td><p>此属性标识尝试自动或手动向目标传递邮件的次数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SCL</strong></p></td>
<td><p><code>SCL</code></p></td>
<td><p>垃圾邮件可信度 (SCL) 属性值指定邮件的 SCL。有效的 SCL 条目是从 0 到 9 的整数。空 SCL 属性值表示邮件尚未经过内容筛选器代理的处理。</p>
<p>此属性包含邮件的垃圾邮件可信度 (SCL) 值。有效 SCL 条目为从 0 到 9 和 -1 的整数。有关详细信息，请参阅<a href="spam-confidence-level-threshold-exchange-2013-help.md">垃圾邮件可信度阈值</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>大小 (KB)</strong></p></td>
<td><p><code>Size</code></p></td>
<td><p>此属性标识邮件的大小。</p></td>
</tr>
<tr class="odd">
<td><p><strong>源 IP</strong></p></td>
<td><p><code>SourceIP</code></p></td>
<td><p>此属性包含向保留队列中邮件的 Exchange 服务器提交邮件的服务器的 IP 地址。该地址可以是远程 SMTP 服务器的 IP 地址或本地 Exchange 服务器的 IP 地址。</p></td>
</tr>
<tr class="even">
<td><p><strong>状态</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>此属性标识当前的邮件状态。邮件可以具有下列状态值之一：</p>
<p><code>Active</code></p>
<p><code>Locked</code></p>
<p><code>None</code></p>
<p><code>Pending Remove</code></p>
<p><code>Pending Suspend</code></p>
<p><code>Ready</code></p>
<p><code>Retry</code></p>
<p><code>Suspended</code></p>
<p>有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;邮件属性&amp;quot;部分。</p></td>
</tr>
<tr class="odd">
<td><p><strong>主题</strong></p></td>
<td><p><code>Subject</code></p></td>
<td><p>此属性标识邮件头的 <code>Subject:</code> 头字段中的邮件主题。</p></td>
</tr>
</tbody>
</table>

