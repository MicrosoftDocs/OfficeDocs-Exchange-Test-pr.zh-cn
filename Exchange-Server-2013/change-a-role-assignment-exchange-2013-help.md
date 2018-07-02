---
title: '更改角色分配: Exchange 2013 Help'
TOCTitle: 更改角色分配
ms:assetid: 0fa77efc-e393-461f-b3c0-232cc56cee85
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335096(v=EXCHG.150)
ms:contentKeyID: 50490013
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 更改角色分配

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

管理角色分配向角色受理人分配一个管理角色。通过更改角色分配，可以对已分配角色的角色受理人所能够更改的对象进行控制。应用到角色分配的管理角色作用域会覆盖角色的隐式写入作用域。但是，角色的隐式读取作用域仍然适用。应用的作用域无法返回角色隐式读取作用域之外的对象。

有关 Microsoft Exchange Server 2013 中管理角色作用域和分配的详细信息，请参阅下列主题：

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

若要了解与角色分配相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的“角色分配”条目。

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


## 您想执行什么操作？

## 使用命令行管理程序启用或禁用某个角色分配

默认情况下，角色分配处于启用状态，这意味着已将关联的角色应用于分配了此角色的角色受理人。如果禁用角色分配，则关联的角色不会应用于角色受理人。

若要启用某个角色分配，请使用以下语法。

    Set-ManagementRoleAssignment <role assignment> -Enabled $true

若要禁用某个角色分配，请使用以下语法。

    Set-ManagementRoleAssignment <role assignment> -Enabled $false

此示例将禁用 Help Desk Assignment 角色分配。

    Set-ManagementRoleAssignment "Help Desk Assignment" -Enabled $false

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335173\(v=exchg.150\))。

## 使用命令行管理程序在角色分配上更改管理角色或角色受理人

无法更改在角色分配上指定的管理角色或角色受理人。如果要使某个角色分配与另一个角色或角色受理人相关联，则必须创建一个新的角色分配，然后删除旧角色分配。有关如何添加和删除角色分配的详细信息，请参阅下列主题：

  - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [从用户或 USG 删除角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

如果已直接对用户或通用安全组 (USG) 创建了分配，则我们建议您考虑使用管理角色组和管理角色分配策略。角色组和分配策略使您能够简化权限模型，并减少需要管理的角色分配数。有关详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 使用命令行管理程序在角色分配上更改预定义相对作用域

可以在角色分配上更改或添加预定义相对作用域。如果添加或更改某个预定义作用域，则任何先前指定的收件人作用域都会从角色分配中删除。有关预定义作用域及其说明的列表，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

若要在角色分配上更改或添加预定义作用域，请使用以下语法。

    Set-ManagementRoleAssignment <assignment name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

此示例将 John 的“分配”角色分配上的预定义作用域更改为 MyDistributionGroups。

    Set-ManagementRoleAssignment "John's Assignment" - RecipientRelativeWriteScope MyDistributionGroups

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335173\(v=exchg.150\))。

## 使用命令行管理程序在角色分配上更改收件人筛选器作用域

可以指定新的基于收件人筛选器的作用域，或更改已应用于此角色分配的基于收件人筛选器的作用域。如果添加某个收件人筛选器作用域，则任何先前定义的收件人作用域都会从角色分配中删除。

若要指定新的基于收件人筛选器的作用域或替换现有作用域，请使用以下语法。

    Set-ManagementRoleAssignment <assignment name> -CustomRecipientWriteScope <role scope name>

此示例将对 Redmond 收件人添加或更改基于收件人筛选器的作用域。

    Set-ManagementRoleAssignment "Redmond Recipient Administrators Assignment" -CustomRecipientWriteScope "Redmond Recipients"

如果要保持与应用于此角色分配相同的基于收件人筛选器的作用域，但又要更改用于匹配收件人对象的收件人筛选器，则需要更改作用域自身的收件人筛选器。有关如何更改作用域的详细信息，请参阅[更改角色范围](change-a-role-scope-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335173\(v=exchg.150\))。

## 使用命令行管理程序在角色分配上更改服务器筛选器或基于列表的配置作用域

可以指定新服务器筛选器或基于列表的配置作用域，或更改已应用于此角色分配的作用域。如果添加或更改配置作用域，则任何先前指定的配置作用域都会从角色分配中删除。

若要指定新配置作用域或替换现有的配置作用域，请使用以下语法。

    Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>

此示例将对 Redmond Servers 添加或更改配置作用域。

    Set-ManagementRoleAssignment "Redmond Administrators Assignment" -CustomConfigWriteScope "Redmond Servers"

如果要保持与应用于此角色分配相同的配置作用域，但又要更改此作用域上的服务器筛选器或服务器列表，则需要对配置作用域自身进行更改。有关如何更改作用域的详细信息，请参阅[更改角色范围](change-a-role-scope-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335173\(v=exchg.150\))。

## 使用命令行管理程序在角色分配上更改数据库筛选器或基于列表的配置作用域

可以指定新数据库筛选器或基于列表的配置作用域，也可以更改已应用于此角色分配的作用域。如果添加或更改配置作用域，则任何先前指定的配置作用域都会从角色分配中删除。

若要指定新配置作用域或替换现有的配置作用域，请使用以下语法。

    Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>

此示例将对 Redmond Databases 添加或更改配置作用域。

    Set-ManagementRoleAssignment "Redmond Database Admins" -CustomConfigWriteScope "Redmond Databases"

如果要保持与应用于此角色分配相同的配置作用域，但又要更改此作用域上的数据库筛选器或数据库列表，则需要对配置作用域自身进行更改。有关如何更改作用域的详细信息，请参阅[更改角色范围](change-a-role-scope-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335173\(v=exchg.150\))。

## 使用命令行管理程序在角色分配上更改组织单位

可以添加新 OU，或更改已应用于此角色分配的 OU。如果指定新 OU，则任何先前指定的收件人作用域都会从角色分配中删除。

若要在角色分配上更改或添加新 OU，请使用以下语法。

    Set-ManagementRoleAssignment <assignment name> -RecipientOrganizationalUnitScope <OU>

此示例将 contoso.com 域中的 Engineering\\Users OU 添加到 Engineering Help Desk 角色分配。

    Set-ManagementRoleAssignment "Engineering Help Desk" -RecipientOrganizationalUnitScope contoso.com/Engineering/Users

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335173\(v=exchg.150\))。

## 使用命令行管理程序更改独占收件人作用域或独占配置作用域

若要更改独占收件人或独占配置作用域，可以使用本主题前面的“使用命令行管理程序在角色分配上更改收件人筛选器作用域”、“使用命令行管理程序在角色分配上更改服务器筛选器或基于列表的配置作用域”和“使用命令行管理程序在角色分配上更改数据库筛选器或基于列表的配置作用域”各节中提供的步骤。唯一差别在于更改独占作用域时，必须指定以下独占参数（取决于是更改独占收件人作用域，还是独占配置作用域）：

  - **独占收件人作用域：** 使用 *ExclusiveRecipientWriteScope* 参数代替 *CustomRecipientWriteScope* 参数。

  - **独占服务器和数据库配置作用域**   使用 *ExclusiveConfigWriteScope* 参数代替 *CustomConfigWriteScope* 参数。

与常规收件人和配置作用域一样，如果添加或更改某个独占作用域，则会替换任何先前定义的收件人或配置作用域。

此示例将更改独占收件人写入作用域。

    Set-ManagementRoleAssignment "Exclusive Executive Users" -ExclusiveRecipientWriteScope "Exclusive Executives"

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335173\(v=exchg.150\))。

