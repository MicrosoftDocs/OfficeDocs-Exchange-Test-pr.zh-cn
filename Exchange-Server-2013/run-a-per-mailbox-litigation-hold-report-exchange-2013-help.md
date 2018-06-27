---
title: '运行每个邮箱的诉讼保留报告: Exchange 2013 Help'
TOCTitle: 运行每个邮箱的诉讼保留报告
ms:assetid: 98c46226-2f48-42c6-a741-34bb5944f519
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150542(v=EXCHG.150)
ms:contentKeyID: 50489772
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 运行每个邮箱的诉讼保留报告

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2012-10-13_

如果您的组织涉及某项法律诉讼，则您可能必须采取步骤以保留可能会用作证据的相关数据（例如电子邮件）。在类似这样的情形中，您可以使用诉讼保留来保留特定人员发送和接收的所有电子邮件，或保留特定时间段内在您的组织中发送和接收的所有电子邮件。有关在将某个邮箱置于诉讼保留时会出现什么情况以及如何启用和禁用诉讼保留的详细信息，请参阅[管理用户邮箱](manage-user-mailboxes-exchange-2013-help.md)中的“邮箱功能”部分。

使用诉讼保留报告可跟踪在给定时间段内对某个邮箱所做的以下类型的更改：

  - 已启用诉讼保留。

  - 已禁用诉讼保留。

对于上述每个更改类型，报告将包含执行更改的用户以及执行更改的日期和时间。

## 在开始之前，您需要知道什么？

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“仅查看管理员审核日志记录”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 使用 EAC 运行诉讼保留报告

1.  在 EAC 中，导航到“合规性管理” \>“审核”。

2.  单击“运行每邮箱诉讼保留报告”。
    
    Microsoft Exchange 将运行有关在过去两周内对任何邮箱所做的诉讼保留更改的报告。

3.  若要查看针对特定邮箱的更改，请在搜索结果窗格中选择相应的邮箱。在详细信息窗格中查看搜索结果。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>要缩小搜索结果的范围吗？选择开始日期、结束日期或同时选择这两个日期，并选择要搜索的特定邮箱。单击“搜索”再次运行此报告。</td>
</tr>
</tbody>
</table>


## 您如何知道这有效？

若要验证是否已经成功运行诉讼保留报告，在指定日期范围内进行诉讼保留更改的邮箱会显示在“搜索结果”窗格中。如果未显示任何结果，则指定日期范围内未发生诉讼保留更改或最近的变更并未生效。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>当邮箱置于诉讼保留时，60 分钟后保留才会生效。</td>
</tr>
</tbody>
</table>

