---
title: '高可用性和站点恢复权限: Exchange 2013 Help'
TOCTitle: 高可用性和站点恢复权限
ms:assetid: 66085107-4d4d-41c3-a425-82314acd9eee
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638136(v=EXCHG.150)
ms:contentKeyID: 50490733
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 高可用性和站点恢复权限

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-11-12_

配置高可用性所需的权限取决于执行的步骤和要运行的 cmdlet。有关高可用性的详细信息，请参阅[高可用性和站点恢复](high-availability-and-site-resilience-exchange-2013-help.md)。

若要了解执行过程或运行 cmdlet 所需的权限，请执行以下操作：

1.  在下表中查找与所要执行的过程或要运行的 cmdlet 最相关的功能。

2.  接下来，查看该功能所需的权限。您必须被分配到其中一个角色组、等效的自定义角色组或等效的管理角色。还可以单击角色组查看其管理角色。如果某个功能列出多个角色组，则您只需要被分配到其中一个角色组就可以使用此功能。有关角色组和管理角色的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

3.  现在运行 **Get-ManagementRoleAssignment** cmdlet 以查看分配给您的角色组或管理角色，以便确定您是否具有管理该功能所需的权限。
    
    > [!NOTE]  
    > 必须分配了 Role Management 管理角色才能运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet。如果没有运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet 的权限，则请求 Exchange 管理员检索分配给您的角色组或管理角色。


如果要将管理一项功能的权限委派给另一个用户，请参阅[委派角色分配](delegate-role-assignments-exchange-2013-help.md)。

## 数据库可用性组权限

您可以使用下表中的功能添加、删除和配置数据库可用性组 (DAG) 的设置。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


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
<td><p>数据库可用性组成员身份</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">数据库可用性组角色</a></p></td>
</tr>
<tr class="even">
<td><p>数据库可用性组属性</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">数据库可用性组角色</a></p></td>
</tr>
<tr class="odd">
<td><p>数据库可用性组</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">数据库可用性组角色</a></p></td>
</tr>
<tr class="even">
<td><p>数据库可用性网络</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">数据库可用性组角色</a></p></td>
</tr>
</tbody>
</table>


## 邮箱数据库副本权限

您可以使用下表中的功能添加、删除、更新和激活邮箱数据库副本。


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
<td><p>数据库切换</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="databases-role-exchange-2013-help.md">数据库角色</a></p></td>
</tr>
<tr class="even">
<td><p>邮箱数据库副本</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">数据库副本角色</a></p></td>
</tr>
<tr class="odd">
<td><p>服务器切换</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="databases-role-exchange-2013-help.md">数据库角色</a></p></td>
</tr>
<tr class="even">
<td><p>更新邮箱数据库副本</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">数据库副本角色</a></p></td>
</tr>
</tbody>
</table>

