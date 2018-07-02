﻿---
title: '帮助中心: Exchange 2013 Help'
TOCTitle: 帮助中心
ms:assetid: e7958752-22e4-4155-a2fc-948099dec6f7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876949(v=EXCHG.150)
ms:contentKeyID: 50491881
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 帮助中心

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

帮助中心 管理角色组是组成 Microsoft Exchange Server 2013 中基于角色的访问控制 (RBAC) 权限模型的多个内置角色组之一。角色组会分配给一个或多个管理角色，这些管理角色拥有执行一组给定任务所需的权限。角色组的成员会获得访问角色组所分配的管理角色的权限。有关角色组的详细信息，请参阅[了解管理角色组](understanding-management-role-groups-exchange-2013-help.md)。

属于 Help Desk 角色组成员的用户可以对 Exchange 2013 收件人执行受限制的收件人管理。

帮助台角色组，默认情况下，使成员可以查看和修改组织中任何用户的Outlook Web App选项。这些选项可能包括修改用户的显示名称、 地址、 电话号码等。它们不包含在Outlook Web App选项，例如修改邮箱的大小或配置邮箱所在的邮箱数据库中不可用的选项。

此角色组的成员只能修改用户可修改的Outlook Web App选项。这意味着，如果用户可以修改他或她显示名称，帮助台角色组的成员还可以修改该用户的显示名称。但是，如果另一个用户不允许修改他或她显示名称，帮助台角色组的成员不能修改该用户的显示名称。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在Outlook Web App的帮助台角色组的成员可以修改的选项强制Exchange管理中心 (EAC) 的限制。帮助台角色组的成员可以访问Exchange命令行管理程序，如果他或她可以修改任何用户的任何Outlook Web App选项。使帮助台角色组的成员，是否它们应该还被赋予访问 Shell，您应仔细考虑。</td>
</tr>
</tbody>
</table>


因为有这么多不同类型的组织，帮助台角色组不能让任何其他任务。相反，可以将管理角色添加到该组角色创建符合组织的需要的技术支持部门角色组。例如，如果您想要能够管理邮箱、 邮件联系人和已启用邮件的用户的帮助台角色组的成员，分配到此角色组邮件收件人管理角色。有关如何将管理角色添加到此角色的组的详细信息，请参阅本主题后面部分中的"角色组自定义"部分。

有关 RBAC 的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 角色组成员身份

如果要向此角色组中添加或从中删除成员，请参阅[管理角色组成员](manage-role-group-members-exchange-2013-help.md)。

默认情况下，只有 Organization Management 角色组的成员可以向此角色组中添加或从员删除成员。有关如何添加其他角色组委派的详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)中的\&quot;添加或删除角色组委派\&quot;一节。

可以使用以下命令查看作为此角色组成员的用户或通用安全组 (USG) 的列表。

    Get-RoleGroupMember "Help Desk"

有关角色组的成员的详细信息，请参阅[管理角色组成员](manage-role-group-members-exchange-2013-help.md)中的[View the members of a role group](manage-role-group-members-exchange-2013-help.md)。

## 角色组自定义

此角色组默认分配管理角色。\&quot;分配给此角色组的管理角色\&quot;一节列出了所包括的角色。您可以向此该角色组中添加或从中删除角色分配，以满足您组织的需要。

Exchange 2013 附带的角色组旨在匹配更精细的任务。通过将角色分配到角色组，就可以使该角色组的成员能够执行与该角色相关联的任务。例如，Journaling 角色可以管理日记代理和日记规则。有关如何将角色分配给角色组的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

分配给此角色组的角色拥有默认管理作用域。管理作用域确定可以由角色组成员查看或修改的 Exchange 对象。可以更改与角色和角色组之间的分配相关联的作用域。例如，如果仅希望角色组的成员能够更改特定组织单位下或特定位置中的收件人，则可能要执行此操作。有关管理作用域的详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

有关如何自定义该角色组的详细信息，请参阅下列主题：

  - [管理角色组](manage-role-groups-exchange-2013-help.md)

  - [管理角色组成员](manage-role-group-members-exchange-2013-help.md)

如果要创建角色组并将部分已分配到该角色组的角色分配到新的角色组，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)中的\&quot;创建角色组\&quot;一节。

## 分配给此角色组的管理角色

下表列出了分配给此角色组的所有管理角色，以及每个角色分配的下列属性：

  - **常规分配：**使角色组成员能够访问由关联管理角色提供的管理角色条目。

  - **委派分配：**使角色组成员能够将指定角色分配给其他角色组、角色分配策略、用户或 USG。

  - **收件人读取作用域：**确定角色组成员允许从 Active Directory 读取的收件人对象。

  - **收件人写入作用域：**确定角色组成员允许在 Active Directory 中修改的收件人对象。

  - **配置读取作用域：**确定角色组成员允许从 Active Directory 读取的配置和服务器对象。

  - **配置写入作用域：**确定角色组成员允许在 Active Directory 中修改的组织对象和服务器对象。

有关角色分配和管理作用域的详细信息，请参阅下列主题：

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

### 分配给此角色组的管理角色

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色</th>
<th>常规分配</th>
<th>委派分配</th>
<th>收件人读取作用域</th>
<th>收件人写入作用域</th>
<th>配置读取作用域</th>
<th>配置写入作用域</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="user-options-role-exchange-2013-help.md">用户选项角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">仅查看收件人角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
</tbody>
</table>

