---
title: '-ContentFilter 参数的可筛选属性: Exchange 2013 Help'
TOCTitle: -ContentFilter 参数的可筛选属性
ms:assetid: cf504a59-1938-489c-bb48-b27b2ac3234e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff601762(v=EXCHG.150)
ms:contentKeyID: 50556674
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# \-ContentFilter 参数的可筛选属性

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-09-10_

本主题列出了 *ContentFilter* 参数的可筛选属性。*ContentFilter* 参数用于将邮件导出到与筛选器匹配的 .pst 文件。*ContentFilter* 参数用在 [New-MailboxExportRequest](https://technet.microsoft.com/zh-cn/library/ff607299\(v=exchg.150\)) cmdlet 中。

## 可筛选属性

*ContentFilter* 参数的许多属性都接受通配符。如果使用通配符，请使用 **-like** 运算符而不是 **-eq** 运算符。**-like** 运算符可用于查找多种类型（如字符串）的模式匹配项，而 **-eq** 运算符可用于查找完全匹配项。

下表包含 *ContentFilter* 参数的可筛选属性列表。此表列出了属性的名称、描述、可接受的值以及语法示例。有关 OPATH 筛选器的详细信息，请参阅[收件人命令行管理程序命令中的筛选器](https://technet.microsoft.com/zh-cn/library/bb124268\(v=exchg.150\))。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>说明</th>
<th>值</th>
<th>示例语法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>All</p></td>
<td><p>此属性返回在任何索引属性中具有特定字符串的所有邮件。例如，如果要导出以&amp;quot;Ayla&amp;quot;为收件人、发件人或在邮件正文中提到该名称的所有邮件，则应使用此属性。</p></td>
<td><p>字符串</p>
<p>通配符</p></td>
<td><pre><code>-ContentFilter {All -like &#39;*Ayla*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Attachment</p></td>
<td><p>此属性返回在附件内容或附件文件名中包含指定字符串的邮件。</p></td>
<td><p>字符串</p>
<p>通配符</p></td>
<td><pre><code>-ContentFilter {Attachment -like &#39;*.jpg&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>BCC</p></td>
<td><p>此属性返回在&amp;quot;密件抄送&amp;quot;字段中具有指定收件人的已发送邮件。</p></td>
<td><p>显示名称</p>
<p>别名</p>
<p>SMTP 地址</p>
<p>LegacyDN</p>
<p>通配符</p></td>
<td><pre><code>-ContentFilter {(BCC -eq &#39;ayla@contoso.com&#39;) -or (BCC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>此属性返回邮件正文中包含指定字符串的邮件。</p></td>
<td><p>字符串</p>
<p>通配符</p></td>
<td><pre><code>-ContentFilter {Body -like &#39;*prospectus*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>此属性返回具有匹配类别的邮件。类别是由用户或收件箱规则设置的。</p></td>
<td><p>字符串</p>
<p>通配符</p></td>
<td><pre><code>-ContentFilter {Category -like &#39;*Blue*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>此属性返回在&amp;quot;抄送&amp;quot;字段中具有指定收件人的已发送邮件。</p></td>
<td><p>显示名称</p>
<p>别名</p>
<p>SMTP 地址</p>
<p>LegacyDN</p>
<p>通配符</p></td>
<td><pre><code>-ContentFilter {(CC -eq &#39;ayla@contoso.com&#39;) -or (CC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Expires</p></td>
<td><p>此属性返回具有指定的过期时间戳的邮件。</p></td>
<td><p>日期时间戳</p></td>
<td><pre><code>-ContentFilter {Expires -lt &#39;01/01/2013&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>HasAttachment</p></td>
<td><p>此属性返回带有或不带附件的邮件。</p></td>
<td><p>布尔值</p>
<p><code>$true</code> 或者<code>$false</code></p></td>
<td><pre><code>-ContentFilter {HasAttachment -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>此属性返回具有指定的重要性级别的邮件。</p></td>
<td><p>0 或者&amp;quot;低&amp;quot;</p>
<p>1 或者&amp;quot;普通&amp;quot;</p>
<p>2 或者&amp;quot;高&amp;quot;</p></td>
<td><pre><code>-ContentFilter {Importance -eq &#39;high&#39;}</code></pre>
<pre><code>-ContentFilter {Importance -eq 2}</code></pre></td>
</tr>
<tr class="even">
<td><p>IsFlagged</p></td>
<td><p>此属性返回已由用户或收件箱规则标记的邮件。</p></td>
<td><p>布尔值</p>
<p><code>$true</code> 或者<code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsFlagged -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>IsRead</p></td>
<td><p>此属性返回用户已阅读或未阅读的邮件。</p></td>
<td><p>布尔值</p>
<p><code>$true</code> 或者<code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsRead -eq $true}</code></pre></td>
</tr>
<tr class="even">
<td><p>MessageKind</p></td>
<td><p>此属性返回指定类型的邮件。</p></td>
<td><p>日历</p>
<p>联系人</p>
<p>Doc</p>
<p>电子邮件</p>
<p>传真</p>
<p>InstantMessage</p>
<p>日记</p>
<p>注意</p>
<p>文章</p>
<p>RSSFeed</p>
<p>任务</p>
<p>语音邮件</p></td>
<td><pre><code>-ContentFilter {MessageKind -eq &#39;Calendar&#39;}</code></pre>
<pre><code>-ContentFilter {MessageKind -ne &#39;Email&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>MessageLocalee</p></td>
<td><p>此属性返回指定区域设置的邮件。</p></td>
<td><p>CultureInfo</p></td>
<td><pre><code>-ContentFilter {MessageLocale -ne &#39;en-US&#39;}</code></pre>
<pre><code>-ContentFilter {MessageLocale -eq &#39;tr-TR&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>此属性返回在&amp;quot;收件人&amp;quot;、&amp;quot;密件抄送&amp;quot;或&amp;quot;抄送&amp;quot;字段中具有指定收件人的邮件。</p></td>
<td><p>显示名称</p>
<p>别名</p>
<p>SMTP 地址</p>
<p>LegacyDN</p>
<p>通配符</p></td>
<td><pre><code>-ContentFilter {(Participants -eq &#39;ayla@contoso.com&#39;) -or (Participants -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>PolicyTag</p></td>
<td><p>此属性返回带有策略标记的邮件。Exchange 存储仍然将策略标记作为 GUID。因此，字符串既可以包含随后由 PR_POLICY_TAG 搜索的显式 GUID 值，也可以包含通配符。</p>
<p>如果提供的值不是 GUID，则命令会使用 Active Directory 信息将名称解析为 GUID。</p></td>
<td><p>字符串</p>
<p>通配符</p></td>
<td><pre><code>-ContentFilter {PolicyTag -ne &#39;00000000-0000-0000-0000-000000000000&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>此属性返回接收的带有指定接收时间戳的邮件。</p></td>
<td><p>日期时间戳</p></td>
<td><pre><code>-ContentFilter {Received -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Received -lt &#39;01/01/2013&#39;) -and (Received -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Sender</p></td>
<td><p>此属性返回接收到的来自指定发件人的邮件。</p></td>
<td><p>显示名称</p>
<p>别名</p>
<p>SMTP 地址</p>
<p>LegacyDN</p>
<p>通配符</p></td>
<td><pre><code>ContentFilter {Sender -eq &#39;tony&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>此属性返回发送的带有指定发送时间戳的邮件。</p></td>
<td><p>日期时间戳</p></td>
<td><pre><code>-ContentFilter {Sent -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Sent -lt &#39;01/01/2013&#39;) -and (Sent -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>此属性返回特定大小的邮件。</p></td>
<td><p>B（字节）</p>
<p>KB（千字节）</p>
<p>MB（兆字节）</p></td>
<td><pre><code>-ContentFilter {Size -gt &#39;10KB&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Subject</p></td>
<td><p>此属性返回邮件主题中包含指定字符串的邮件。</p></td>
<td><p>字符串</p>
<p>通配符</p></td>
<td><pre><code>-ContentFilter {Subject -like &#39;*meeting*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>To</p></td>
<td><p>此属性返回在&amp;quot;收件人&amp;quot;字段中具有指定收件人的已发送邮件。</p></td>
<td><p>显示名称</p>
<p>别名</p>
<p>SMTP 地址</p>
<p>LegacyDN</p>
<p>通配符</p></td>
<td><pre><code>-ContentFilter {To -eq &#39;aylakol&#39;}</code></pre></td>
</tr>
</tbody>
</table>

