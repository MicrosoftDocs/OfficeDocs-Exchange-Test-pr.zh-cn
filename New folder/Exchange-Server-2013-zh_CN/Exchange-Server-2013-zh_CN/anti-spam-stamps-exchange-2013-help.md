---
title: '反垃圾邮件标记: Exchange 2013 Help'
TOCTitle: 反垃圾邮件标记
ms:assetid: 28d3a5c2-8509-4b25-9876-763536e77c27
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996878(v=EXCHG.150)
ms:contentKeyID: 50490236
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 反垃圾邮件标记

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

当邮件通过对来自 Internet 的入站邮件进行筛选的反垃圾邮件功能时，反垃圾邮件标记通过对邮件应用诊断元数据或标记（如发件人特定的信息、问题验证结果和内容筛选结果），帮助你诊断与垃圾邮件相关的问题。有三个反垃圾邮件标记：网络钓鱼可能性等级标记、垃圾邮件可信度标记和发件人 ID 标记。

可以将反垃圾邮件标记用作诊断工具来确定将对个人邮箱中收到的误报和可疑垃圾邮件进行什么操作。

## 查看反垃圾邮件标记

可以使用 Microsoft Outlook 来查看反垃圾邮件标记。有关详细信息，请参阅[在 Outlook 中查看反垃圾邮件标记](view-anti-spam-stamps-in-outlook-exchange-2013-help.md)。

## 了解反垃圾邮件报告

反垃圾邮件报告是已应用于电子邮件的反垃圾邮件筛选器结果的摘要报告。内容筛选器代理将此标记以 X-header 的形式应用于邮件信封，如下所示。

    X-MS-Exchange-Organization-Antispam-Report: DV:<DATVersion>;CW:CustomList;PCL:PhishingVerdict <verdict>;P100:PhishingBlock;PP:Presolve;SID:SenderIDStatus <status>;TIME:<SendReceiveDelta>;MIME:MimeCompliance 

下表描述了可在反垃圾邮件报告中出现的筛选器信息。

> [!NOTE]
> 反垃圾邮件报告只显示已应用于特定邮件的筛选器的信息。通常，反垃圾邮件报告不包含下表中列出的所有信息。例如，你可能会收到以下反垃圾邮件报告：<code>DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures</code>。


### 反垃圾邮件报告中的筛选器信息

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>标记</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SID</p></td>
<td><p>发件人 ID (SID) 标记基于发件人策略框架 (SPF)，该框架授权在电子邮件中使用域。SPF 在邮件信封中显示为 <code>Received-SPF</code>。发件人 ID 评估过程会为邮件生成发件人 ID 状态。此状态可以作为下列值之一返回：</p>
<ul>
<li><p><strong>Pass</strong>   IP 地址和假设负责地址 (PRA) 都通过了发件人 ID 验证检查。</p></li>
<li><p><strong>Neutral</strong>   发布的发件人 ID 数据明显不具有决定性。</p></li>
<li><p><strong>Soft fail</strong>   PRA 的 IP 地址可能在禁止的集合内。</p></li>
<li><p><strong>Fail</strong>   IP 地址不允许使用；在传入邮件中未找到任何 PRA，或发件人域不存在。</p></li>
<li><p><strong>None</strong>   发件人的 DNS 中没有任何已发布的 SPF 数据。</p></li>
<li><p><strong>TempError</strong> 出现临时 DNS 失败，例如 DNS 服务器不可用。</p></li>
<li><p><strong>PermError</strong>   DNS 记录无效，例如，记录格式错误。</p></li>
</ul>
<p>发件人 ID 标记在邮件信封中显示为一个 X-Header，如下所示：</p>
<pre><code>X-MS-Exchange-Organization-SenderIdResult:&lt;status&gt;</code></pre>
<p>有关发件人 ID 的详细信息，请参阅<a href="sender-id-exchange-2013-help.md">发件人 ID</a>。</p></td>
</tr>
<tr class="even">
<td><p>DV</p></td>
<td><p>DAT 版本 (DV) 标记指示扫描邮件时所使用的垃圾邮件定义文件的版本。</p></td>
</tr>
<tr class="odd">
<td><p>SA</p></td>
<td><p>签名操作 (SA) 标记指示由于在邮件中找到签名而恢复或删除此邮件。</p></td>
</tr>
<tr class="even">
<td><p>SV</p></td>
<td><p>签名 DAT 版本 (SV) 标记指示扫描邮件时所使用的签名文件的版本。</p></td>
</tr>
<tr class="odd">
<td><p>PCL</p></td>
<td><p>网络钓鱼可能性等级 (PCL) 标记根据邮件的内容显示邮件分级，并在内容筛选器代理处理邮件时应用。此状态可以作为下列值之一返回：</p>
<ul>
<li><p><strong>Neutral</strong>   邮件内容可能不是仿冒。</p></li>
<li><p><strong>Suspicious</strong>   邮件内容可能会被冒仿。</p></li>
</ul>
<p>PCL 值的范围从 1 到 8。一个评级为 1 到 3 的 PCL 返回 <code>Neutral</code> 的状态。这意味着邮件的内容可能不是网络钓鱼。一个评级为 4 到 8 的 PCL 返回 <code>Suspicious</code> 的状态。这意味着邮件可能是网络钓鱼。</p>
<p>这些值用于确定 Outlook 对邮件执行的操作。Outlook 使用 PCL 标记来阻止可疑邮件的内容。</p>
<p>PCL 标记在邮件信封中显示为一个 X-header，如下所示：</p>
<pre><code>X-MS-Exchange-Organization-PCL:&lt;status&gt;</code></pre></td>
</tr>
<tr class="even">
<td><p>SCL</p></td>
<td><p>邮件的垃圾邮件可信度 (SCL) 标记根据邮件内容显示邮件的分级。内容筛选器代理使用 Microsoft SmartScreen 技术评估邮件内容，并为每个邮件分配 SCL 分级。SCL 值介于 0 到 9 之间，其中 0 表示是垃圾邮件的可能性最低，9 表示是垃圾邮件的可能性最高。Exchange 和 Outlook 执行的操作取决于你的 SCL 阈值设置。</p>
<p>SCL 标记在邮件信封中显示为一个 X-header，如下所示：</p>
<pre><code>X-MS-Exchange-Organization-SCL:&lt;status&gt;</code></pre>
<p>有关 SCL 阈值和操作的详细信息，请参阅<a href="spam-confidence-level-threshold-exchange-2013-help.md">垃圾邮件可信度阈值</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CW</p></td>
<td><p>邮件的自定义权值 (CW) 标记指示邮件包含未批准的字词或短语，以及这些未批准的字词或短语的 SCL 值或权值已应用于 SCL 的最终得分：</p>
<ul>
<li><p>未批准的短语或阻止短语具有最大的权值，可以将 SCL 得分更改为 9。</p></li>
<li><p>已批准的字词或短语或允许短语具有最小的权值，可以将 SCL 得分更改为 0。</p></li>
</ul>
<p>有关如何将批准的和未批准的字词或短语添加到内容筛选代理的详细信息,请参阅<a href="manage-content-filtering-exchange-2013-help.md">管理内容筛选</a>。</p></td>
</tr>
<tr class="even">
<td><p>PP</p></td>
<td><p>预先解决的问题 (PP) 标记指示：如果发件人的邮件中包含一个已解决计算邮戳的、基于 Outlook 电子邮件邮戳的有效验证功能，则此发件人不太可能是恶意发件人。在这种情况下，内容筛选器代理将降低 SCL 分级。</p>
<p>如果启用了电子邮戳验证功能，并且以下任一条件为真时，内容筛选器代理将不会更改 SCL 分级：</p>
<ul>
<li><p>入站邮件中不包含计算邮戳标头。</p></li>
<li><p>计算邮戳标头无效。</p></li>
</ul>
<p>有关邮戳验证功能的详细信息，请参阅<a href="content-filtering-exchange-2013-help.md">内容筛选</a>。</p></td>
</tr>
<tr class="odd">
<td><p>TIME:TimeBasedFeatures</p></td>
<td><p>TIME 标记指示发送邮件的时间和接收邮件的时间之间有一个明显的时间延迟。使用 TIME 标记可确定邮件的最终 SCL 分级。</p></td>
</tr>
<tr class="even">
<td><p>MIME:MIMECompliance</p></td>
<td><p>MIME 标记指示电子邮件与 MIME 不兼容。</p></td>
</tr>
<tr class="odd">
<td><p>P100:PhishingBlock</p></td>
<td><p>P100 标记指示邮件包含一个在仿冒定义文件中出现的 URL。</p></td>
</tr>
<tr class="even">
<td><p>IPOnAllowList</p></td>
<td><p>IPOnAllowList 标记指示发件人的 IP 地址位于 IP 允许列表中。有关 IP 允许列表的详细信息，请参阅<a href="http://go.microsoft.com/fwlink/?linkid=268732">了解连接筛选</a>。</p></td>
</tr>
<tr class="odd">
<td><p>MessageSecurityAntispamBypass</p></td>
<td><p>MessageSecurityAntispamBypass 标记指示没有对邮件内容进行筛选，并且已授予发件人绕过反垃圾邮件筛选器的权限。</p></td>
</tr>
<tr class="even">
<td><p>SenderBypassed</p></td>
<td><p>SenderBypassed 标记指示内容筛选器代理不会对来自此发件人的邮件进行任何内容筛选。有关详细信息，请参阅<a href="manage-content-filtering-exchange-2013-help.md">管理内容筛选</a>。</p></td>
</tr>
<tr class="odd">
<td><p>AllRecipientsBypassed</p></td>
<td><p>AllRecipientsBypassed 标记指示邮件中列出的所有收件人都符合下列条件之一：</p>
<ul>
<li><p>收件人邮箱上的 <em>AntispamBypassedEnabled</em> 参数设置为 <code>$true</code>。这是只能由管理员使用 <strong>Set-Mailbox</strong> cmdlet 设置的每个收件人的设置。</p></li>
<li><p>邮件发件人列于收件人的 Outlook 安全发件人列表中。有关“安全发件人列表”的详细信息，请参阅<a href="manage-safelist-aggregation-exchange-2013-help.md">管理安全列表聚合</a>。</p></li>
<li><p>内容筛选器代理不会对发送给此收件人的邮件进行任何内容筛选。有关收件人例外的详细信息，请参阅<a href="manage-content-filtering-exchange-2013-help.md">管理内容筛选</a>。</p></li>
</ul></td>
</tr>
</tbody>
</table>

