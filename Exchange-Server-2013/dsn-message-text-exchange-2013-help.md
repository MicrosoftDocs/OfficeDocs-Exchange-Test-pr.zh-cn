---
title: 'DSN 邮件文本: Exchange 2013 Help'
TOCTitle: DSN 邮件文本
ms:assetid: eae4a050-5ecb-4c87-b377-74edb93a5995
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125135(v=EXCHG.150)
ms:contentKeyID: 50491871
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DSN 邮件文本

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

您可以在 Microsoft Exchange Server 2013 中的自定义传递状态通知 (DSN) 邮件中加入文本，并可将该文本格式化为 HTML 格式。

您可以包括任何您想要显示给 DSN 邮件的收件人的信息。例如，您可以包括 DSN，联系信息服务台，以及支持部门的 Web 站点的链接的详细的说明。每个 DSN 邮件可以包含最多为 512 个字符。

因为 DSN 邮件可以显示以 html 格式，您可以嵌入 HTML 格式设置标记的 DSN 文本中。例如，如果您想要将 DSN 邮件中的某些文本加粗，括起的中文 \< B \> 和 \< /B \> HTML 标记。下表提供了一些可以在 DSN 邮件文本中使用的有效 HTML 标记的示例。

### 在 DSN 邮件中使用的有效 HTML 标记

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>HTML 标记</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;B&gt;</p></td>
<td><p>粗体开始</p></td>
</tr>
<tr class="even">
<td><p>&lt;/B&gt;</p></td>
<td><p>粗体结束</p></td>
</tr>
<tr class="odd">
<td><p>&lt;A HREF=&quot;url&quot;&gt;</p></td>
<td><p>超链接开始</p></td>
</tr>
<tr class="even">
<td><p>&lt;/A&gt;</p></td>
<td><p>超链接结束</p></td>
</tr>
<tr class="odd">
<td><p>&lt;BR&gt;</p></td>
<td><p>链接断开</p></td>
</tr>
<tr class="even">
<td><p>&lt;EM&gt;</p></td>
<td><p>斜体开始</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/EM&gt;</p></td>
<td><p>斜体结束</p></td>
</tr>
<tr class="even">
<td><p>&lt;P&gt;</p></td>
<td><p>段落开始</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/P&gt;</p></td>
<td><p>段落结束</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>默认情况下，Exchange 发送 HTML DSN 邮件，但您可以配置 Exchange HTML DSN 将消息发送给内部发件人、 外部发件人，或这两者。若要配置此行为，请修改<em>InternalDsnSendHtml</em>参数，使用<strong>Set-TransportService</strong>命令使用<em>ExternalDsnSendHtml</em>参数。<br />
如果将<em>InternalDsnSendHtml</em>参数设置为<code>$false</code>，Exchange 将禁止 DSN 邮件发送给内部发件人中的 HTML 标记。如果将<em>ExternalDsnSendHtml</em>参数设置为<code>$false</code>，Exchange 将禁止 DSN 邮件发送到外部发件人中的 HTML 标记。</td>
</tr>
</tbody>
</table>


Exchange 在 DSN 邮件文本中使用的下列字符有特殊含义：

  - 大于符号 (\>)

  - 大于符号 (\<)

  - 与号 (&)

  - 引号 (")

这些字符用于确定 HTML 标记的开始和结束位置，并应显示给发件人的文本位置启动和停止。如果您想要在您的 DSN 邮件显示这些字符，必须在下表中使用的转义码。

例如，如果想要显示邮件 `"Please contact the Help Desk at <1234>."`，则必须向 DSN 邮件文本添加 `"Please contact the Help Desk at &lt;1234&gt;." `。

### DSN 邮件字符转义代码

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>转义代码</th>
<th>字符</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp;lt;</p></td>
<td><p>&lt;</p></td>
</tr>
<tr class="even">
<td><p>&amp;gt;</p></td>
<td><p>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;</p></td>
<td><p>&quot;</p></td>
</tr>
<tr class="even">
<td><p>&amp;amp;</p></td>
<td><p>&amp;</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果 DSN 邮件文本包含引号 （&quot;），如<code>&lt;A HREF=&quot;url&quot;&gt;</code>中包含 HTML 标记，必须围绕整个 DSN 邮件文本中使用单引号 （'） 引起来。如果使用双引号引起周围整个 DSN 邮件文本和 HTML 标记前后，将收到一条错误消息。</td>
</tr>
</tbody>
</table>

