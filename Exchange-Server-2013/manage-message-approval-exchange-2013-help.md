---
title: '管理邮件审批: Exchange 2013 Help'
TOCTitle: 管理邮件审批
ms:assetid: 43a89f71-8002-4cb0-b3c8-1c2b2597f227
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd297936(v=EXCHG.150)
ms:contentKeyID: 50490388
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理邮件审批

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-05-04_

有时在发送邮件之前再多检查一遍会非常有用。作为 Exchange 管理员，您可以树立这一流程。该流程称为*仲裁*，负责审批的用户称为*仲裁人*。根据需要审批的邮件，您可以使用下面两种方法之一：

  - 更改通讯组属性

  - 创建邮件流规则

本文介绍：

  - 如何决定使用哪种审批方法

  - 审批过程的工作原理

要了解如何实施常见方案，请参阅[常见邮件审批方案](common-message-approval-scenarios-exchange-2013-help.md)。

## 如何决定使用哪种审批方法

下面将对两种邮件审批方法进行比较。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>要执行什么操作？</th>
<th>方法</th>
<th>第一步</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>创建仲裁通讯组，发送到该组的所有邮件都必须经过审批。</p></td>
<td><p>为通讯组设立邮件审批。</p></td>
<td><p>转到 Exchange 管理中心 (EAC) &gt;“收件人”&gt;“组” ，编辑通讯组，然后选择“邮件审批”。</p></td>
</tr>
<tr class="even">
<td><p>对匹配特定条件或发送给特定用户的邮件设置审批要求。</p></td>
<td><p>使用“转发邮件以进行审批”操作创建传输规则。</p>
<p>您可以指定邮件条件，包括文本模式、发件人和收件人。您的条件也可以包含例外。</p></td>
<td><p>转到 EAC &gt;“邮件流”&gt;“规则”。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 审批过程的工作原理

当某人向需要审批的个人或组发送邮件时，如果他们使用 Outlook Web Access，则会收到邮件可能延迟的通知。

![显示邮件审批通知的邮件](images/Dd297936.80e2e5f1-0a1e-4c37-9076-794581155405(EXCHG.150).png "显示邮件审批通知的邮件")

仲裁人收到请求批准或拒绝邮件的电子邮件。邮件文本中包含批准或拒绝邮件的按钮，附件包含要审阅的原始邮件。

![审批请求邮件，包括附件](images/Dd297936.bf517f5a-b10e-40df-a48a-403b395b5962(EXCHG.150).png "审批请求邮件，包括附件")

仲裁人可以采取以下三项操作之一：

![显示邮件审批选项的工作流](images/Dd297936.dc7a6ca9-c67d-487a-8713-4d628e07f4b3(EXCHG.150).png "显示邮件审批选项的工作流")

1.  如果得到批准，邮件将发送给预期的原始收件人。原始发件人不会收到通知。

2.  如果被拒绝，将向发件人发送拒绝邮件。仲裁人可以添加解释：
    
    ![拒绝通知，包含审阅人的注释](images/Dd297936.a663d36a-c67d-4155-b8f6-4b5dc8e105d9(EXCHG.150).png "拒绝通知，包含审阅人的注释")  

3.  如果审批者删除或忽略审批邮件，将向发件人发送过期邮件。在 Exchange Online 中过期时间为两天，在 Exchange Server 2013 中为五天。（在 Exchange Server 2013 中，您可以更改此时间。）

等待审批的邮件会临时存储在称为*仲裁邮箱*的系统邮箱中。在仲裁人决定批准或拒绝邮件、删除审批邮件或者让审批邮件过期之前，原始邮件将保留在仲裁邮箱中。

返回顶部

## 问题和回答

**通讯组的仲裁人和所有者之间有何区别？**

通讯组的所有者负责管理通讯组成员身份，但无法仲裁发送给它的邮件。例如，可能某位 IT 员工是名为“所有员工”的通讯组的所有者，但只有人力资源经理才能被设置为仲裁人。

**当仲裁人或审批者向通讯组发送邮件时，会发生什么？**

邮件直接发送到通讯组，跳过审批流程。

**当只有一部分收件人需要审批时，会发生什么？**

您可以向只有一部分收件人需要审批的收件人组发送邮件。请考虑一封发送给 12 个收件人的邮件，其中一个收件人为仲裁通讯组。邮件自动拆分成两个副本。一个邮件直接发送给 11 个不需要审批的收件人，另一个邮件提交到仲裁通讯组的审批流程。如果邮件针对多个仲裁收件人，将为每个仲裁收件人自动创建一个单独的邮件副本，每个副本都需经过相应的审批流程。

**如果通讯组包含需要审批的仲裁收件人，应该怎么办？**

通讯组可能包含也需要审批的仲裁收件人。在这种情况下，发送到该通讯组的邮件得到批准后，该通讯组中的每个仲裁收件人将具有单独的审批过程。但是，在发送到仲裁通讯组的邮件得到批准后，也可以启用通讯组成员的自动审批。要实现这一点，可使用 [Set-DistributionGroup](https://technet.microsoft.com/zh-cn/library/bb124955\(v=exchg.150\)) cmdlet 上的 *BypassNestedModerationEnabled* 参数。

**如果我们有自己的 Exchange 服务器，此过程是否会不同？**

默认情况下，每个 Exchange 组织使用一个仲裁邮箱。如果您具有自己的 Exchange 服务器且需要更多的仲裁邮箱实现负载平衡，请按照[管理邮件审批并进行故障排除](manage-and-troubleshoot-message-approval-exchange-2013-help.md)中有关添加仲裁邮箱的说明操作。仲裁邮箱是系统邮箱，不需要 Exchange 许可证。

> [!NOTE]  
> <strong>如果您使用 Exchange 2007：</strong>Microsoft Exchange Server 2007 不支持仲裁收件人。如果将某封发送给仲裁通讯组的邮件在 Exchange 2007 集线器传输服务器上展开，该邮件将绕过仲裁过程，传递给通讯组的所有成员。如果您的 Exchange 组织中有 Exchange 2007 集线器传输服务器，您需要指定一台 Exchange Server 2013 邮箱服务器作为仲裁通讯组的展开服务器。这样可确保所有发送给通讯组的邮件都能得到仲裁。


返回顶部

## 需要更多帮助？

[管理邮件流规则](manage-mail-flow-rules-exchange-2013-help.md)

[Exchange 2013 的 Exchange 命令行管理程序快速参考](exchange-management-shell-quick-reference-for-exchange-2013-exchange-2013-help.md)

[Exchange Online PowerShell](https://technet.microsoft.com/zh-cn/library/jj200677\(v=exchg.150\))

