---
title: '常见的附件阻止方案: Exchange Online Help'
TOCTitle: 常见的附件阻止方案
ms:assetid: 5c576439-d55b-4c7f-90ed-a7f72cbb16c2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn950026(v=EXCHG.150)
ms:contentKeyID: 65285929
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 常见的附件阻止方案

 

_**适用于：** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**上一次修改主题：** 2017-02-23_

为了满足法律或合规性要求，或者为了满足特定的业务需求，您的组织可能需要阻止或拒绝某些类型的邮件。下面的一些示例展示了您可以使用传输规则在 Exchange 中设置的用于阻止所有附件的常见方案：

  -  Example 1: Block messages with attachments, and notify the sender

  -  Example 2: Notify intended recipients when an inbound message is blocked

  -  Example 3: Modify the subject line for notifications

  -  Example 4: Apply a rule with a time limit

有关如何阻止特定附件的其他示例，请参阅：

  - [使用传输规则检查邮件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013)

  - [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/zh-cn/library/jj919236\(v=exchg.150\)) (Exchange Online, Exchange Online Protection)

恶意软件筛选器包括常见附件类型筛选器。在 Exchange 管理中心 (EAC) 中，转到\&quot;**保护**\&quot;，然后单击\&quot;**新建**\&quot;(![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")) 来添加筛选器。在 Exchange Online 门户中，转到\&quot;**保护**\&quot;，然后选择\&quot;**恶意软件筛选器**\&quot;。

若要开始实现其中一个应用场景来拦截某些类型邮件，请执行以下操作：

1.  登录 Exchange 管理中心。

2.  转到\&quot;邮件流\&quot;\>\&quot;规则\&quot;。

3.  单击\&quot;**新建**\&quot;(![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标"))，然后选择\&quot;**新建规则**\&quot;。

4.  在\&quot;**名称**\&quot;框中为该规则指定名称，然后单击\&quot;**更多选项**\&quot;。

5.  选择相应的条件和操作。

**注意：** 在 EAC 中，你可以输入的最小附件大小为 1 KB，这样应该会检测大多数附件。但是，如果要检测每个任意大小的可能附件，则需要在 EAC 中创建规则后使用 PowerShell 将附件大小调整为 1 字节。若要了解如何在本地 Exchange 组织中打开 Exchange 命令行管理程序，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。若要了解如何使用 Windows PowerShell 连接到 Exchange Online，请参阅[连接到 Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554)。若要了解如何使用 Windows PowerShell 连接到 Exchange Online Protection，请参阅[连接到 Exchange Online Protection PowerShell](https://go.microsoft.com/fwlink/p/?linkid=627290)。

将 *\<Rule Name\>* 替换为现有规则的名称，然后运行下列命令将附件大小设置为 1 字节：

    Set-TransportRule -Identity "<Rule Name>" -AttachmentSizeOver 1B

将附件大小调整为 1 字节后，EAC 中的规则显示的值为 **0.00 KB**。

## 示例 1：阻止包含附件的邮件，并通知发件人

如果您不希望组织中的人员发送或接收附件，则可以将传输规则设置为阻止包含附件的所有邮件。

在此示例中，发向组织或从组织发出的所有包含附件的邮件都会遭到拦截。

![阻止所有附件的规则](images/Dn950026.38094183-166f-4ba5-a9cf-242e7d0f4e04(EXCHG.150).png "阻止所有附件的规则")

如果您仅希望阻止邮件，则不妨设置为在与此规则匹配时停止处理规则。向下滚动规则对话框，然后选中\&quot;停止处理其他规则\&quot;复选框。

## 示例 2：在阻止入站邮件时通知预定收件人

如果您想拒绝邮件，但也希望让预定收件人知道所发生的情况，则可以使用\&quot;使用邮件通知收件人\&quot;操作。

您可以在通知邮件中添加占位符，以便包含原始邮件的信息。必须将占位符放在两个百分号 (%%) 之中。当通知邮件发送时，占位符就会被替换为原始邮件中的信息。您还可以在邮件中使用基本的 HTML，如 \<br\>、\<b\>、\<i\> 和 \<img\>。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>信息类型</strong></p></td>
<td><p><strong>占位符</strong></p></td>
</tr>
<tr class="even">
<td><p>邮件的发件人。</p></td>
<td><p>%%From%%</p></td>
</tr>
<tr class="odd">
<td><p>列于&amp;quot;收件人&amp;quot;行上的收件人。</p></td>
<td><p>%%To%%</p></td>
</tr>
<tr class="even">
<td><p>列于&amp;quot;抄送&amp;quot;行上的收件人。</p></td>
<td><p>%%Cc%%</p></td>
</tr>
<tr class="odd">
<td><p>原始邮件的主题。</p></td>
<td><p>%%Subject%%</p></td>
</tr>
<tr class="even">
<td><p>原始邮件的邮件头。 这类似于为原始邮件生成的传递状态通知 (DSN) 中的邮件头列表。</p></td>
<td><p>%%Headers%%</p></td>
</tr>
<tr class="odd">
<td><p>原始邮件的发送日期。</p></td>
<td><p>%%MessageDate%%</p></td>
</tr>
</tbody>
</table>


在此示例中，包含附件并发送给您组织的内部人员的所有邮件都会遭到阻止，并且收件人会收到通知。

![用于在某封入站邮件被阻止时通知收件人的规则](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "用于在某封入站邮件被阻止时通知收件人的规则")

## 示例 3：修改通知的主题行

向收件人发送通知时，主题行就是原始邮件的主题。如果您想修改主题，更方便收件人理解，则必须使用以下两个传输规则：

  - 第一个规则将\&quot;无法送达\&quot;一词添加到包含附件的所有邮件的主题开头。

  - 第二个规则阻止邮件，并使用原始邮件的新主题向发件人发送通知邮件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>这两个规则必须具有完全相同的条件。由于规则是按顺序进行处理，因此第一个规则先添加&amp;quot;无法送达&amp;quot;一词，然后第二个规则再阻止邮件并通知收件人。</td>
</tr>
</tbody>
</table>


下面展示了第一个规则（如果您想向主题添加\&quot;无法送达\&quot;一词的话）：

![在未送达邮件中添加附件的规则](images/Dn950026.2552b0bd-c69d-48b4-9e69-267fcaf20e70(EXCHG.150).png "在未送达邮件中添加附件的规则")

第二个规则执行阻止和通知操作（来自示例 2 的同一规则）：

![用于在某封入站邮件被阻止时通知收件人的规则](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "用于在某封入站邮件被阻止时通知收件人的规则")

## 示例 4：应用具有时间限制的规则

如果遇到恶意软件爆发，则您不妨应用具有时间限制的规则，以便暂时阻止附件。例如，以下规则具有开始和结束日期、时间：

![显示时间限制的规则](images/Dn950026.bdc8c4d8-72fa-4c5b-97f2-5fe76d50e643(EXCHG.150).png "显示时间限制的规则")

## 另请参阅


[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\))  


[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)  
[Exchange Online Protection 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/dn271424\(v=exchg.150\))

