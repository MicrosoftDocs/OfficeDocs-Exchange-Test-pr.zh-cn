---
title: '使用数据库作用域控制自动邮箱分发: Exchange 2013 Help'
TOCTitle: 使用数据库作用域控制自动邮箱分发
ms:assetid: 8eaff177-2251-4c8b-8570-c91a77d0a6fc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff628332(v=EXCHG.150)
ms:contentKeyID: 50491015
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用数据库作用域控制自动邮箱分发

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-04-07_

自动邮箱分发是 Microsoft Exchange Server 2013 中的一种功能，可在您未显式指定数据库时，随机选择邮箱数据库以存储新邮箱或移动的邮箱。当您要允许初级管理员或技术支持人员创建邮箱而无需了解应在哪些邮箱数据库上创建邮箱时，此功能可能会十分有用。

可以使用数据库管理作用域控制自动邮箱分发可以选择的邮箱数据库。在将数据库作用域应用于某个管理员时，该管理员只能使用与定义的数据库作用域匹配的数据库。因为自动邮箱分发使用当前用户的上下文，所以它也会受到应用于管理员的数据库作用域的约束。

有关自动邮箱分发、数据库作用域和角色分配的详细信息，请参阅下列主题：

  - [自动邮箱分发](automatic-mailbox-distribution-exchange-2013-help.md)

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

要查找与作用域相关的其他管理任务吗？请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该过程的时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的“管理作用域”条目。

  - 您必须使用命令行管理程序执行这些过程。

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


## 您该如何做？

## 步骤 1：创建数据库作用域

在此步骤中，需决定要在数据库作用域中包含的数据库。此外，还需决定是否要指定数据库的静态列表，或是否要创建仅包含与指定条件匹配的数据库的数据库筛选器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>与数据库作用域关联的角色分配仅应用到连接到运行 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更高版本或者 Exchange 2013 的服务器的用户。如果分配了与数据库作用域关联的角色分配的用户连接到之前的 Exchange 2010 SP1 服务器，则角色分配不会应用到此用户，并且不会将角色分配提供的任何权限授予此用户。</td>
</tr>
</tbody>
</table>


## 使用数据库列表作用域

如果要定义应包含在此作用域中的邮箱数据库的静态列表，请使用数据库列表。使用以下语法创建数据库列表作用域。

    New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>

本示例将创建仅适用于数据库 Database 1、Database 2 和 Database 3 的作用域。

    New-ManagementScope -Name "Accounting databases" -DatabaseList "Database 1", "Database 2", "Database 3"

有关详细的语法和参数信息，请参阅 [New-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd335137\(v=exchg.150\))。

## 使用数据库筛选器作用域

如果要创建仅包含与指定条件匹配的数据库的动态数据库作用域，请使用数据库筛选器。如果您不想在创建数据库作用域后对其进行管理，并且已为组织定义了可标识特定邮箱数据库集合的标准值，则此方法可能十分有用。

有关可筛选的数据库属性的列表，请参阅[了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)。

使用以下语法创建数据库筛选器作用域。

    New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>

本示例将创建一个作用域，该作用域包含数据库的 **Name** 属性中含有字符串“ACCT”的所有数据库。

    New-ManagementScope -Name "Accounting Databases" -DatabaseRestrictionFilter { Name -Like '*ACCT*' }

有关语法和参数的详细信息，请参阅 [New-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd335137\(v=exchg.150\))。

## 步骤 2：将数据库作用域添加到管理角色分配

创建作用域后，必须将其添加到新建或现有的管理角色分配。建议您使用管理角色组控制管理权限，因此此步骤中的示例使用名为 Accounting Administrators 的示例角色组。有关如何创建角色组的详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

在使用数据库作用域将角色分配给某个角色组之后，该角色组的成员将只能在作用域中包含的数据库上创建邮箱，并且只能将邮箱移动到这些数据库。

有关可以分配给角色组的内置角色的列表，请参阅[内置管理角色](built-in-management-roles-exchange-2013-help.md)。

## 添加新角色分配

如果刚创建了角色组并且需要向其中添加角色，请使用此过程。

使用下面的语法可使用新数据库作用域，在要分配的管理角色与新角色组之间创建角色分配。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <database scope name>

此示例使用 Accounting Databases 数据库作用域，在 Mail Recipients 和 Mail Recipient Creation 角色与 Accounting Administrators 角色组之间创建角色分配。

    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipients" -CustomConfigWriteScope "Accounting Databases"
    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipient Creation" -CustomConfigWriteScope "Accounting Databases"

有关详细的语法和参数信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 修改现有角色分配

如果您具有一个现有角色组，并且该角色组已在它与您要应用新数据库作用域的角色之间具有角色分配，请使用此过程。

此过程使用管道进行传输。有关详细信息，请参阅[管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))。

使用下面的语法可修改您要应用数据库作用域的管理角色与现有角色组之间的角色分配。

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> | Set-ManagementRoleAssignment -CustomConfigWriteScope <database scope name>

此示例将 Accounting Databases 数据库作用域添加到已分配给 Accounting Administrators 角色组的 Mail Recipients 和 Mail Recipient Creation 角色。

    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipients" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"
    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipient Creation" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\)) 和 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335173\(v=exchg.150\))。

## 步骤 3：向角色组添加成员（如果适用）

如果要向角色组添加成员，请参阅[管理角色组成员](manage-role-group-members-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果向此角色组添加成员以限制他们可以在哪些数据库上创建用户或将邮箱移动到哪些数据库，请确保他们不是可以授予额外权限的其他角色组的成员。</td>
</tr>
</tbody>
</table>


## 步骤 4：从角色组删除成员（如果适用）

如果已将成员添加到新角色组（该角色组限制他们可以在哪些数据库上创建邮箱或将邮箱移动到哪些数据库），并且他们是具有其他权限的另一个角色组的成员，请从旧角色组删除他们。有关详细信息，请参阅[管理角色组成员](manage-role-group-members-exchange-2013-help.md)。

