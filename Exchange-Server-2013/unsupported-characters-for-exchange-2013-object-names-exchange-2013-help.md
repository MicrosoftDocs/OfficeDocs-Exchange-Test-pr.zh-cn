---
title: 'Exchange 2013 对象名称的不受支持字符: Exchange 2013 Help'
TOCTitle: Exchange 2013 对象名称的不受支持字符
ms:assetid: 76fa4e23-f0f6-473b-9227-70ded907578f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn169553(v=EXCHG.150)
ms:contentKeyID: 54652289
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 对象名称的不受支持字符

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

本文介绍 Exchange 2013 的对象名或组件名中不能使用的字符。当在 Exchange 2013 中创建对象名或组件名时，即使您能够使用不受支持的字符创建对象，这些名称也不能包含不受支持的字符。此外，如果尝试导入或连接其名称包含不受支持字符的对象，则您将收到错误消息，或可能发生意外行为。

## 不受支持的字符

下表列出与 Exchange 相关的对象或组件名称中不支持使用的字符。该表还列出使用不受支持字符时可能发生问题的应用场景。请注意，该表中列出的每个对象的最大长度为 64 个字符。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 对象或组件</th>
<th>Exchange 应用场景</th>
<th>不受支持的字符</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>电子邮件域名</p></td>
<td><p>简单邮件传输协议 (SMTP) 连接器</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>连接器地址空间的主机名</p></td>
<td><p>邮件流</p></td>
<td><p><code>..</code>（两个句点）</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 服务器的主机名</p></td>
<td><p>SMTP</p></td>
<td><p><code>_</code>（下划线）</p></td>
</tr>
<tr class="even">
<td><p>组织或站点名称</p></td>
<td><p>运行安装程序或移动邮箱</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>组织内部目录名</p></td>
<td><p>目录</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹树名</p></td>
<td><p>查看并创建公用文件夹</p></td>
<td><p><code>: ;</code></p></td>
</tr>
<tr class="odd">
<td><p>收件人名称</p></td>
<td><p>SMTP</p></td>
<td><p><code>' &quot;</code></p></td>
</tr>
<tr class="even">
<td><p>收件人策略 SMTP 地址</p></td>
<td><p>查看公用文件夹层次结构</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>收件人策略 SMTP 地址主机名</p></td>
<td><p>邮件流</p></td>
<td><p><code>..</code>（两个句点）</p></td>
</tr>
<tr class="even">
<td><p>站点内部目录名</p></td>
<td><p>查看公用文件夹层次结构</p></td>
<td><p><code>? ( ) *</code></p></td>
</tr>
<tr class="odd">
<td><p>智能主机名</p></td>
<td><p>SMTP</p></td>
<td><p>前导或尾随空格</p></td>
</tr>
</tbody>
</table>

