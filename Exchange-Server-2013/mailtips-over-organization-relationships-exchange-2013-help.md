---
title: '有关组织关系的邮件提示: Exchange Online Help'
TOCTitle: 有关组织关系的邮件提示
ms:assetid: 1784256f-abe1-4503-b8c4-26d544b73452
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ670165(v=EXCHG.150)
ms:contentKeyID: 50490096
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 有关组织关系的邮件提示

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

Microsoft Exchange Server 2013允许您使用 Microsoft Exchange Online 或其他Exchange组织配置的组织关系。建立一个组织的关系，可以增强用户体验，在处理与其他组织。例如，可以共享忙 / 闲数据、 配置安全邮件流和跨这两个组织启用邮件跟踪。

## 控制邮件提示访问级别

您可能想要限制某些类型的邮件提醒。可以允许所有邮件提醒要返回或允许只会防止生成 Ndr 的有限的集。与**Set-OrganizationRelationship** cmdlet 的*MailTipsAccessLevel*参数，可以配置该设置。下表显示了该组织关系返回邮件提醒。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>邮件提示</th>
<th>当访问级别设置为&amp;quot;全部&amp;quot;时邮件提示是否可用？</th>
<th>当访问级别设置为&amp;quot;有限&amp;quot;时邮件提示是否可用？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>大型受众</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>自动答复</p></td>
<td><p>是</p>
<p>如果为内部指定收件人的远程域，则会显示内部自动答复。否则，将显示外部自动答复。</p></td>
<td><p>是</p>
<p>显示外部自动答复。</p></td>
</tr>
<tr class="odd">
<td><p>仲裁收件人</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>超大邮件</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>受限制的收件人</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>邮箱已满</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>自定义邮件提示</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>外部收件人</p></td>
<td><p>是</p>
<p>如果为内部指定的远程域的收件人，则此 MailTip 即被隐含。否则，将返回外部 MailTip。</p></td>
<td><p>是</p>
<p>如果为内部指定的远程域的收件人，则此 MailTip 即被隐含。否则，将返回外部 MailTip。</p></td>
</tr>
</tbody>
</table>


有关如何配置邮件提示访问级别的详细步骤，请参阅[针对组织关系管理邮件提示](manage-mailtips-for-organization-relationships-exchange-2013-help.md)。

## 控制邮件提示访问作用域

通过组织关系启用邮件提醒和`All`、 特定收件人的邮件提醒，邮箱已满、 自动答复和自定义邮件提醒设置的访问级别，为所有用户返回。但是，您可能只想允许对一组特定的用户这些邮件提醒。例如，如果与合作伙伴建立的组织的关系，可以使用该合作伙伴的用户只允许这些邮件提醒。

为此，您需要首先创建一个组，然后添加要共享特定收件人的邮件提醒到该组的所有用户。然后，您可以指定该组的组织之间的关系。

在实施这种限制之后，客户端访问服务器首先验证的收件人在收到邮件提醒查询其是否为该组的一部分。如果收件人是此组的成员，客户端访问服务器将返回代理包括特定收件人的邮件提醒所有邮件提醒。否则他们不会在其答复中包括特定收件人的邮件提醒。

有关如何配置邮件提示访问级别的详细步骤，请参阅[针对组织关系管理邮件提示](manage-mailtips-for-organization-relationships-exchange-2013-help.md)。

