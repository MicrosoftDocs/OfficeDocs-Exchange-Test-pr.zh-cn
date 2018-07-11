---
title: '角色管理权限: Exchange 2013 Help'
TOCTitle: 角色管理权限
ms:assetid: cb9591c4-fbb3-4199-8007-6bbfdfd5a2e9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638186(v=EXCHG.150)
ms:contentKeyID: 50491552
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 角色管理权限

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

执行管理角色配置任务所需的权限视所执行的过程或要运行的 cmdlet 而定。有关管理角色的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

若要了解执行过程或运行 cmdlet 所需的权限，请执行以下操作：

1.  在下表中查找与所要执行的过程或要运行的 cmdlet 最相关的功能。

2.  接下来，查看该功能所需的权限。您必须被分配到其中一个角色组、等效的自定义角色组或等效的管理角色。还可以单击角色组查看其管理角色。如果某个功能列出多个角色组，则您只需要被分配到其中一个角色组就可以使用此功能。有关角色组和管理角色的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

3.  现在运行 **Get-ManagementRoleAssignment** cmdlet 以查看分配给您的角色组或管理角色，以便确定您是否具有管理该功能所需的权限。
    
    > [!NOTE]
    > 必须分配了 Role Management 管理角色才能运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet。如果没有运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet 的权限，则请求 Exchange 管理员检索分配给您的角色组或管理角色。


如果要将管理一项功能的权限委派给另一个用户，请参阅[委派角色分配](delegate-role-assignments-exchange-2013-help.md)。

## 角色管理权限

可以使用下表中的功能对管理角色组、角色、分配策略、分配、用于定义可应用于管理员和最终用户的权限的作用域进行管理。分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>管理角色</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>未确定范围的管理角色</p></td>
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">无作用域的角色管理角色</a>管理角色</p></td>
</tr>
<tr class="odd">
<td><p>角色组</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>分配策略</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>角色分配</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>管理作用域</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>管理角色项</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>旧版权限</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Active Directory 拆分权限</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>

> [!important]
> 要运行带有 <em>PrepareAD</em> 和 <em>ActiveDirectorySplitPermissions</em> 参数的 <code>setup.exe</code> 命令，所用帐户必须是 Schema Admins 和 Enterprise Administrators 组的成员。

</td>
</tr>
</tbody>
</table>

