---
title: '在 Exchange 中删除和重新创建默认发现邮箱: Exchange 2013 Help'
TOCTitle: 在 Exchange 中删除和重新创建默认发现邮箱
ms:assetid: 4bde0b00-bdf7-44b4-ba64-aa062bc10ca2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn750894(v=EXCHG.150)
ms:contentKeyID: 62371346
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Exchange 中删除和重新创建默认发现邮箱

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-05-04_

您可以使用 Exchange 命令行管理程序删除默认发现邮箱、重新创建，然后向其分配权限。

## 为何需要执行此操作？

在 Exchange Server 2013 和 Exchange Online 中，默认发现邮箱的大小上限为 50 GB。它用于存储就地电子数据展示搜索结果。在大小限制更改之前，组织可以将存储配额增加到超过 50 GB。因此，发现邮箱可以增加到超过 50 GB。大于 50 GB 的默认发现邮箱存在三个问题：

  - 不受支持。

  - 无法迁移到 Office 365。

  - 如果默认发现邮箱位于 Exchange Server 2010 中，则无法升级到 Exchange Server 2013。

如何解决此问题取决于您是否要保存超过 50 GB 的默认发现邮箱的搜索结果。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>是否要保存搜索结果？</th>
<th>执行操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>否</p></td>
<td><p>按照本主题中的步骤删除默认发现邮箱，然后重新创建。</p></td>
</tr>
<tr class="even">
<td><p>是</p></td>
<td><p>按照<a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">减小 Exchange 中发现邮箱的大小</a>中的步骤执行操作。</p></td>
</tr>
</tbody>
</table>


## 使用 Exchange 命令行管理程序 删除并重新创建默认发现邮箱

> [!NOTE]
> 您无法使用 Exchange 管理中心 (EAC)，因为发现邮箱无法在 EAC 中显示。


1.  运行以下命令删除默认发现邮箱。
    
        Remove-Mailbox "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}"

2.  在要求您确认是否要删除邮箱和相应 Active Directory 用户对象的消息中，键入 **Y**，然后按 Enter 键。
    
    当您在下一步创建发现邮箱时，将在 Active Directory 中创建一个新的用户对象。

3.  运行以下命令重新创建默认发现邮箱。
    
        New-Mailbox -Name "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -Alias "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -DisplayName "Discovery Search Mailbox" -Discovery

4.  运行以下命令分配“发现管理”角色组权限，以打开默认发现邮箱和查看搜索结果。
    
        Add-MailboxPermission "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User "Discovery Management" -AccessRights FullAccess -InheritanceType all

