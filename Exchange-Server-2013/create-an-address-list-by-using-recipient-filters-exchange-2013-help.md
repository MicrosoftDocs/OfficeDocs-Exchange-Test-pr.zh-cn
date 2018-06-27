---
title: '使用收件人筛选器创建地址列表: Exchange Online Help'
TOCTitle: 使用收件人筛选器创建地址列表
ms:assetid: 8eabea64-97c6-40af-b61c-9b6a125cbdf1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123718(v=EXCHG.150)
ms:contentKeyID: 50491155
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用收件人筛选器创建地址列表

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2014-12-16_

本主题介绍了如何使用收件人筛选器创建地址列表。有关地址列表的详细信息，请参阅[地址列表](address-lists-exchange-2013-help.md)。

有关地址列表的更多管理任务，请参阅[地址列表程序](address-list-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的\&quot;地址列表\&quot;条目。

  - 默认情况下，在 Exchange Online 中，地址列表角色不会分配给任何角色组。若要使用需要地址列表角色的任意 cmdlet，您需要向角色组添加此角色。有关详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)主题中的\&quot;向角色组添加角色\&quot;部分。

  - 若要使用 *RecipientFilter* 参数创建自定义筛选器，必须为自定义筛选器指定一个字符串。命令行管理程序将 OPATH 用于筛选语法。OPATH 是一种用于查询对象数据源的查询语言。

  - 您不能使用 Exchange 管理中心 (EAC) 执行此过程，必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序通过收件人筛选器创建地址列表

此示例将为所有位于华盛顿或俄勒冈州的拥有 Exchange 邮箱的用户创建一个新的地址列表。

    New-AddressList -Name "Pacific Northwest Mailboxes" -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

此示例为具有 Exchange 邮箱并且以 `AgencyB` 作为 *CustomAttribute15* 参数值的所有用户创建一个地址列表。

    New-AddressList -Name "AgencyB" -RecipientFilter {(RecipientType -eq 'UserMailbox') -and (CustomAttribute15 -like *AgencyB*)}

有关语法和参数的详细信息，请参阅 [New-AddressList](https://technet.microsoft.com/zh-cn/library/aa996912\(v=exchg.150\))。

