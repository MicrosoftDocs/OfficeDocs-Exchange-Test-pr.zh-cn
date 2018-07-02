---
title: '为电子数据展示保存密件抄送和展开的通讯组收件人: Exchange Online Help'
TOCTitle: 为电子数据展示保存密件抄送和展开的通讯组收件人
ms:assetid: eb8ddf15-0080-457e-9d83-e73e193da334
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn770225(v=EXCHG.150)
ms:contentKeyID: 62516667
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为电子数据展示保存密件抄送和展开的通讯组收件人

 

_**适用于：**Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**上一次修改主题：**2017-06-19_

适当地保存、 诉讼封存，和[Office 365 保留策略](http://go.microsoft.com/fwlink/?linkid=827811)（在Office 365 安全与合规中心中创建） 允许您保留邮箱内容以满足法规遵从性和 eDiscovery 要求。有关收件人的信息直接阐述在收件人和抄送字段默认情况下，所有的消息中包含一条消息，但您的组织可能需要搜索并重现有关邮件的所有收件人的详细信息的能力。这包括：

  - **使用邮件密件抄送字段输入地址的收件人：**密件抄送收件人存储在发件人邮箱的邮件中，但不包含于发送给收件人的邮件标头中。

  - **展开的通讯组收件人：**接收此邮件的收件人，因为他们是以\&quot;收件人\&quot;、\&quot;抄送\&quot;或\&quot;密件抄送\&quot;字段在邮件中输入地址的通讯组成员。

Exchange Online和Exchange Server 2013 （累积更新 7 及更高版本） 保留有关密件抄送以及展开的通讯组收件人的信息。可以通过使用Exchange 管理中心 (EAC) 中的适当 eDiscovery 搜索或安全与合规中心中的内容搜索来搜索这些信息。

## 如何保留密件抄送收件人和展开的通讯组收件人

如上文所述，有关密收件人信息与发件人邮箱中的邮件存储。此信息索引和 eDiscovery 搜索到可用并保存。

展开的通讯组收件人的信息存储消息之后将邮箱放在原位保存或诉讼封存。在Office 365， Office 365保留策略应用到一个邮箱时也存储此信息。在发送消息的时间确定通讯组成员身份。消息存储的扩展的收件人列表不受对组成员身份的更改后发送消息。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>有关信息…</th>
<th>存储在...</th>
<th>默认情况下存储？</th>
<th>可访问…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp;quot;收件人&amp;quot;和&amp;quot;抄送&amp;quot;收件人</p></td>
<td><p>发件人和收件人邮箱中的邮件属性。</p></td>
<td><p>是</p></td>
<td><p>发件人、收件人和合规部主管</p></td>
</tr>
<tr class="even">
<td><p>密件抄送收件人</p></td>
<td><p>发件人邮箱中的邮件属性。</p></td>
<td><p>是</p></td>
<td><p>发件人和合规部主管</p></td>
</tr>
<tr class="odd">
<td><p>展开的通讯组收件人</p></td>
<td><p>发件人邮箱中的邮件属性。</p></td>
<td><p>不。展开的通讯组收件人信息存储之后邮箱放在原位保存或诉讼封存，或分配给Office 365保留策略。</p></td>
<td><p>合规部主管</p></td>
</tr>
</tbody>
</table>


## 搜索发送给密件抄送以及展开的通讯组收件人的邮件

在搜索发送给收件人的邮件时，目前，电子数据展示搜索结果包括发送给收件人为通讯组成员的邮件。下表显示的方案中，邮件发送至电子数据展示搜索中返回的密件抄送以及展开的通讯组收件人。

方案 1：John 是美国销售通讯组的成员。当 Bob 通过通讯组直接或间接发送一封邮件给 John 时，此表将显示电子数据展示搜索结果。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>当您在 Bob 的邮箱中搜索发送的邮件时…</th>
<th>并与邮件一起发送…</th>
<th>结果包含邮件？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>收件人：John</p></td>
<td><p>处于&amp;quot;收件人&amp;quot;中的 John</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>收件人：John</p></td>
<td><p>处于&amp;quot;收件人&amp;quot;中的美国销售</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>收件人：美国销售</p></td>
<td><p>处于&amp;quot;收件人&amp;quot;中的美国销售</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>抄送：John</p></td>
<td><p>处于&amp;quot;抄送&amp;quot;中的 John</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>抄送：John</p></td>
<td><p>处于&amp;quot;抄送&amp;quot;中的美国销售</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>抄送：美国销售</p></td>
<td><p>处于&amp;quot;抄送&amp;quot;中的美国销售</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


方案 2：Bob 发送一封电子邮件给 John（收件人/抄送）和 Jack（通过通讯组直接或间接密件抄送）。下表显示了电子数据展示搜索结果。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>当搜索…</th>
<th>对于发送的邮件…</th>
<th>结果包含邮件？</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bob 的邮箱</p></td>
<td><p>收件人/抄送：John</p></td>
<td><p>是</p></td>
<td><p>显示一个表明 Jack 被密件抄送的指示。</p></td>
</tr>
<tr class="even">
<td><p>Bob 的邮箱</p></td>
<td><p>密件抄送：Jack</p></td>
<td><p>是</p></td>
<td><p>显示一个表明 Jack 被密件抄送的指示。</p></td>
</tr>
<tr class="odd">
<td><p>Bob 的邮箱</p></td>
<td><p>密件抄送：Jack（通过通讯组）</p></td>
<td><p>是</p></td>
<td><p>发送邮件时会展开密件抄送通讯组成员列表，电子数据展示搜索结果预览、导出和日志中会显示此列表。</p></td>
</tr>
<tr class="even">
<td><p>John 的邮箱</p></td>
<td><p>收件人/抄送：John</p></td>
<td><p>是</p></td>
<td><p>不会显示密件抄送收件人。</p></td>
</tr>
<tr class="odd">
<td><p>John 的邮箱</p></td>
<td><p>密件抄送：Jack（直接或通过通讯组）</p></td>
<td><p>否</p></td>
<td><p>密件抄送信息不存储在发送给收件人的邮件中。您必须搜索发件人的邮箱。</p></td>
</tr>
<tr class="even">
<td><p>Jack 的邮箱</p></td>
<td><p>收件人/抄送：John（直接或通过通讯组）</p></td>
<td><p>是</p></td>
<td><p>收件人/抄送信息包含在发送给所有收件人的邮件中。</p></td>
</tr>
<tr class="odd">
<td><p>Jack 的邮箱</p></td>
<td><p>密件抄送：Jack（直接或通过通讯组）</p></td>
<td><p>否</p></td>
<td><p>密件抄送信息不存储在发送给收件人的邮件中。您必须搜索发件人的邮箱。</p></td>
</tr>
</tbody>
</table>


## 常见问题

**问： 密件抄送收件人信息存储何时何地？**  
A.密件抄送收件人信息保留默认情况下，在原始邮件中发件人的邮箱中。如果密件抄送收件人是通讯组，通讯组成员资格只展开如果发件人邮箱被保留或分配给Office 365保留策略。

**问： 何时、 何地是展开的通讯组列表收件人分组存储？**  
A.组成员身份在发送消息的时间展开。展开的通讯组的成员的列表存储在原始邮件中发件人的邮箱中。发件人邮箱必须在原地保留，诉讼封存，或分配给Office 365保留策略。

**问：收件人/抄送收件人可以看到被密件抄送的收件人吗？**  
答：此信息并不包含在邮件标头中，对收件人/抄送收件人不可见。发件人可以看到其邮箱中所存储原始邮件中的密件抄送字段。搜索发件人邮箱时，合规部主管可以看到此信息。

**问： 如何确保展开的通讯组收件人始终保留的？**  
A。若要确保展开的通讯组的成员始终保留邮件， [保留所有邮箱](place-all-mailboxes-on-hold-exchange-2013-help.md)或创建组织范围Office 365保留策略。

**问：支持哪些类型的组？**  
答：支持通讯组、已启用邮件的安全组和动态通讯组。

**问：邮件中展开和存储的通讯组收件人数量存在限制吗？**  
答：最多保留 10000 个通讯组成员。

**问：支持嵌套通讯组吗？**  
答：支持，可展开 25 层级嵌套通讯组。

**问：密件抄送和展开的通讯组收件人信息在哪里可见？**  
答：当执行电子数据展示搜索时，密件抄送和展开的通讯组收件人信息对合规部主管可见。复制到发现邮箱或导出到 PST 文件以及搜索结果电子数据展示日志的搜索结果中包含密件抄送和展开的通讯组收件人。密件抄送收件人信息在搜索预览中也可用。

**问：如果通讯组中的一个成员在组织的全局地址列表 (GAL) 中被隐藏会怎样？**  
答：没有任何影响。如果收件人在 GAL 中被隐藏，它们仍包括在展开的通讯组的收件人列表中。

