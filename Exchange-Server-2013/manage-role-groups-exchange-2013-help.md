---
title: '管理角色组: Exchange 2013 Help'
TOCTitle: 管理角色组
ms:assetid: ab9b7a3b-bf67-4ba1-bde5-8e6ac174b82c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657480(v=EXCHG.150)
ms:contentKeyID: 50491288
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理角色组

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-10-08_

本主题显示如何添加、删除、复制和查看 Microsoft Exchange Server 2013 中的管理角色组。它还显示如何添加、删除和列出角色组上的管理角色，以及如何更改角色组上的管理作用域和委派。有关 Exchange 2013 中角色组的详细信息，请参阅[了解管理角色组](understanding-management-role-groups-exchange-2013-help.md)。

有关角色组相关的其他管理任务，请参阅 [权限](permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：5 到 10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;角色组\&quot;条目。

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

## 创建角色组

如果要自定义可以分配给用户组的权限，请新建一个自定义管理角色组。

## 使用 EAC 创建角色组

1.  在 Exchange 管理中心 (EAC) 中，导航到\&quot;权限\&quot;\>\&quot;管理员角色\&quot;，然后单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在\&quot;新建角色组\&quot;窗口中，提供新角色组的名称。

3.  您可以现在选择要分配给角色组的角色以及要添加到角色组的成员，也可以另选时间执行此操作。

4.  选择要应用于新角色组的写入作用域。

5.  单击\&quot;保存\&quot;创建角色组。

## 使用命令行管理程序创建角色组

示例

## 您如何知道这有效？

若要验证是否已成功创建了角色组，请执行以下操作：

1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  验证新的角色组是否显示在角色组列表中，然后选择它。

3.  验证在新角色组上指定的成员、分配的角色和作用域是否在角色组详细信息窗格中列出。

## 复制角色组

## 使用 EAC 复制角色组

如果您拥有的角色组包含您希望授予用户的权限，但您希望在无须手动添加所有其他角色的情况下应用其他管理作用域，或删除或添加一个或两个管理角色，则您可以复制现有角色组。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果已经使用 Exchange 命令行管理程序在角色组上配置多个管理角色作用域或独占作用域，则无法使用 EAC 复制角色组。如果已经在角色组上配置多个作用域或独占作用域，则必须使用本主题中后面的命令行管理程序复制角色组。有关管理角色作用域的详细信息，请参阅<a href="understanding-management-role-scopes-exchange-2013-help.md">了解管理角色作用域</a>。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  选择要复制的角色组，然后单击\&quot;复制\&quot;![复制图标](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "复制图标")。

3.  在\&quot;新建角色组\&quot;窗口中，提供新角色组的名称。

4.  审查已复制到新角色组的角色。根据需要添加或删除角色。

5.  审查写入作用域，并根据需要更改。

6.  审查已复制到新角色组的成员。根据需要添加或删除成员。

7.  单击\&quot;保存\&quot;创建角色组。

## 使用命令行管理程序复制无作用域的角色组

1.  请使用以下语法将想要复制的角色组存储在变量中。
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  请使用以下语法创建新角色组，并将成员添加到该角色组，然后指定可以将该角色组委派给其他用户的用户。
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -Members <member1, member2, member3...> -ManagedBy <user1, user2, user3...>

例如，使用以下命令复制\&quot;Organization Management\&quot;角色组并将新角色组命名为\&quot;Limited Organization Management\&quot;。将添加成员 Isabelle、Carter 和 Lukas，并可由 Jenny 和 Katie 进行委派。

    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Limited Organization Management" -Roles $RoleGroup.Roles -Members Isabelle, Carter, Lukas -ManagedBy Jenny, Katie

创建新角色组后，可以添加或删除角色、更改角色的角色分配范围以及执行其他操作。

有关语法和参数的详细信息，请参阅 [Get-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638115\(v=exchg.150\)) 和 [New-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638181\(v=exchg.150\))。

## 使用命令行管理程序复制有自定义作用域的角色组

1.  请使用以下语法将想要复制的角色组存储在变量中。
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  请使用以下语法创建有自定义作用域的新角色组。
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuraiton scope name>

例如，使用以下命令复制\&quot;Organization Management\&quot;角色组并创建名为\&quot;Vancouver Organization Management\&quot;的新角色组，该角色组具有\&quot;Vancouver Users\&quot;收件人作用域和\&quot;Vancouver Servers configuration\&quot;配置作用域。

    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Vancouver Organization Management" -Roles $RoleGroup.Roles -CustomRecipientWriteScope "Vancouver Users" -CustomConfigWriteScope "Vancouver Servers"

使用本主题中前面的使用命令行管理程序复制没有作用域的角色组中所示的 *Members* 参数创建角色组后，也可以向该角色组添加成员。有关管理作用域的详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

创建新角色组后，可以添加或删除角色、更改角色的角色分配范围以及执行其他任务。

有关语法和参数的详细信息，请参阅 [Get-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638115\(v=exchg.150\)) 和 [New-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638181\(v=exchg.150\))。

## 使用命令行管理程序复制有 OU 作用域的角色组

1.  请使用以下语法将想要复制的角色组存储在变量中。
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  请使用以下语法创建有自定义作用域的新角色组。
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope <OU name>

例如，使用以下命令复制\&quot;Recipient Management\&quot;角色组并创建名为\&quot;Toronto Recipient Management\&quot;的新角色组，该角色组允许在\&quot;Toronto Users\&quot;OU 中仅管理用户。

    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Toronto Recipient Management" -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope "contoso.com/Toronto Users"

使用本主题中前面的使用命令行管理程序复制没有作用域的角色组中所示的 *Members* 参数创建角色组后，也可以向该角色组添加成员。有关管理作用域的详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

创建新角色组后，可以添加或删除角色、更改角色的角色分配范围以及执行其他操作。

有关语法和参数的详细信息，请参阅 [Get-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638115\(v=exchg.150\)) 和 [New-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638181\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功复制了角色组，请执行以下操作：

1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  验证已复制的角色组是否显示在角色组列表中，然后选择它。

3.  验证在已复制的角色组上指定的成员、分配的角色和作用域是否在角色组详细信息窗格中列出。

## 删除角色组

如果不再需要所创建的角色组，则可以将其删除。删除角色组时，也将删除角色组和管理角色之间的管理角色分配。管理角色不会被删除。如果用户依赖于此角色组来访问某个功能，则该用户将不再拥有访问此功能的权限。无法删除内置角色组。

## 使用 EAC 删除角色组

1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  选择要删除的角色组，然后单击\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

3.  验证您是否要删除所选择的角色组，如果是，则在警告框中回答\&quot;是\&quot;。

## 使用命令行管理程序删除角色组

示例

## 查看角色组

您可以查看角色组的列表，也可以查看有关组织中存在的特定角色组的详细信息。

## 使用 EAC 查看角色组列表和角色组详细信息

1.  在 EAC 中，导航到\&quot;**权限**\&quot;\>\&quot;**管理员角色**\&quot;。这里列出了你组织中的所有角色组。

2.  选择一个角色组，以查看角色组上配置的成员、分配的角色和作用域。

## 使用命令行管理程序查看角色组列表和角色组详细信息

示例

## 向角色组添加角色

将管理角色添加到角色组是向一组管理员或专家用户授予权限的最好且最简单的方式。如果要使作为角色组成员的用户能够管理某个功能，需要将管理该功能的管理角色添加到角色组。在添加角色之后，即会向角色组成员授予该角色所提供的权限。

## 使用 EAC 将管理角色添加到角色组

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果已经使用命令行管理程序在角色组上配置多个管理角色作用域或独占作用域，则无法使用 EAC 向角色组中添加角色。如果已在角色组上配置多个作用域或独占作用域，则必须使用本主题后面的命令行管理程序步骤将角色添加到角色组。有关管理角色作用域的详细信息，请参阅<a href="understanding-management-role-scopes-exchange-2013-help.md">了解管理角色作用域</a>。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  选择要向其添加角色的角色组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;角色\&quot;部分中，选择要添加到角色组的角色。

4.  当您将角色添加到角色组后，单击\&quot;保存\&quot;。

## 使用命令行管理程序创建无作用域的角色分配

可以在角色和角色组之间创建无作用域的角色分配。这样做时，角色的隐式读取和隐式写入作用域都适用。

使用以下语法可将没有任何作用域的角色分配给角色组。如果不指定角色分配名称，则会自动创建一个角色分配名称。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name>

此示例将 Transport Rules 管理角色分配给 Seattle Compliance 角色组。

    New-ManagementRoleAssignment -SecurityGroup "Seattle Compliance" -Role "Transport Rules"

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 使用命令行管理程序创建具有预定义作用域的角色分配

如果预定义作用域满足你的业务要求，则可以将该作用域应用于角色分配，而不是新建一个角色分配。有关预定义作用域及其说明的列表，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

有关角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

使用以下语法可将角色分配给具有预定义作用域的角色组。如果不指定角色分配名称，则会自动创建一个角色分配名称。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientRelativeWriteScope < MyGAL | MyDistributionGroups | Organization | Self >

此示例将 Message Tracking 角色分配给 Enterprise Support 角色组，并应用 Organization 预定义作用域。

    New-ManagementRoleAssignment -SecurityGroup "Enterprise Support" -Role "Message Tracking" -RecipientRelativeWriteScope Organization

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 使用命令行管理程序创建具有基于收件人筛选器的作用域的角色分配

如果创建了基于收件人筛选器的作用域，则需要使用 *CustomRecipientWriteScope* 参数将该作用域包含在用于向角色组分配角色的命令中。

创建具有收件人写入作用域的角色分配时，也可以包含配置写入作用域。

有关角色分配和作用域的详细信息，请参阅下列主题：

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

使用以下语法可将角色分配给具有基于收件人筛选器的作用域的角色组。如果不指定角色分配名称，则会自动创建一个角色分配名称。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomRecipientWriteScope <role scope name>

此示例将 Message Tracking 角色分配给 Seattle Recipient Admins 角色组，并应用 Seattle Recipients 作用域。

    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Message Tracking" -CustomRecipientWriteScope "Seattle Recipients"

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 使用命令行管理程序创建具有配置作用域的角色分配

如果创建了基于服务器配置筛选器的作用域、基于数据库配置筛选器的作用域或基于列表的作用域，则需要使用 *CustomConfigWriteScope* 参数将该作用域包含在用于向角色组分配角色的命令中。

创建具有配置写入作用域的角色分配时，也可以包含收件人写入作用域。

有关角色分配和管理作用域的详细信息，请参阅下列主题：

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

使用以下语法可将角色分配到具有配置作用域的角色组。如果不指定角色分配名称，则会自动创建一个角色分配名称。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <role scope name>

此示例将 Databases 角色分配给 Seattle Server Admins 角色组，并应用 Seattle Servers 作用域。

    New-ManagementRoleAssignment -SecurityGroup "Seattle Server Admins" -Role "Databases" -CustomConfigWriteScope "Seattle Servers"

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 使用命令行管理程序创建具有 OU 作用域的角色分配

如果要将角色的写入作用域限定为某个 OU，则可以直接在 *RecipientOrganizationalUnitScope* 参数中指定该 OU。

有关角色分配和管理作用域的详细信息，请参阅下列主题：

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

使用以下命令可将角色分配给角色组，并将角色的写入作用域限制为特定的 OU。如果不指定角色分配名称，则会自动创建一个角色分配名称。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientOrganizationalUnitScope <OU>

此示例将 Mail Recipients 角色分配给 Seattle Recipient Admins 角色组，并将该分配的作用域限定为 Contoso.com 域中的 Sales\\Users OU。

    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功将角色添加到角色组，请执行以下操作：

1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  选择要将角色添加到的角色组。在角色组详细信息窗格中，验证添加的角色是否列出。

## 从角色组中删除角色

从管理角色组中删除角色是吊销授予给一组管理员或专家用户的权限的最佳且最简单的方式。如果你不希望管理员或专家用户拥有管理某一功能的权限，则将管理角色从管理这些权限的管理角色组中删除。删除角色后，角色组的成员将不再拥有管理该功能的权限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>一些角色组（例如 组织管理 角色组）会限制可以从角色组中删除哪些角色。有关详细信息，请参阅<a href="understanding-management-role-groups-exchange-2013-help.md">了解管理角色组</a>。<br />
如果管理员为另一个角色组（该角色组包含授予权限以管理功能的管理角色）的成员，您需要从其他角色组中删除此管理员，或从其他角色组中删除授予管理功能权限的角色。</td>
</tr>
</tbody>
</table>


## 使用 EAC 从角色组中删除管理角色

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果已经使用命令行管理程序在角色组上配置多个作用域或独占作用域，则无法使用 EAC 从角色组中删除角色。如果你已经在角色组上配置多个作用域或独占作用域，你必须使用本主题中稍后介绍的命令行管理程序步骤将角色从角色组中删除。有关管理角色作用域的详细信息，请参阅<a href="understanding-management-role-scopes-exchange-2013-help.md">了解管理角色作用域</a>。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  选择要从中删除角色的角色组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;角色\&quot;部分中，选择要从中删除角色组的角色。

4.  从角色组中删除角色后，单击\&quot;保存\&quot;。

## 使用命令行管理程序从角色组中删除角色

你可以通过使用 **Get-ManagementRoleAssignment** cmdlet 检索关联管理角色分配，然后通过管道将返回的角色分配传输到 **Remove-ManagementRoleAssignment** cmdlet，来将角色从角色组中删除。除非你要同时删除委派角色分配和常规角色分配，否则请指定 *Delegating* 参数来指定你要删除常规角色分配还是委派角色分配。

有关常规角色分配和委派角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

此过程使用管道进行传输。有关管道传输的详细信息，请参阅[管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))。

若要从角色组删除角色，请使用下列语法。

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment

本示例将通讯组角色（该角色使管理员能够管理通讯组）从 Seattle Recipient Administrators 角色组中删除。因为我们要删除提供通讯组管理权限的角色分配，所以将 *Delegating* 参数设置为 `$False`，以仅返回常规角色分配。

    Get-ManagementRoleAssignment -RoleAssignee "Seattle Recipient Administrators" -Role "Distribution Groups" -Delegating $false | Remove-ManagementRoleAssignment

有关语法和参数的详细信息，请参阅 [Remove-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351205\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功从角色组中删除角色，请执行以下操作：

1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  选择从中删除了角色的角色组。在角色组详细信息窗格中，验证删除的角色是否不再列出。

## 更改角色组的作用域

角色组和角色之间的管理角色分配包含管理作用域，管理作用域确定该角色组成员可用的对象。通过更改角色组上的写入作用域，可以更改角色组成员可创建、更改或删除的对象。不能更改角色组上的读取作用域。

Exchange 2013 包括在未创建自定义作用域时，默认应用于角色分配的作用域。如果你要对角色组上的角色分配使用自定义作用域，则必须首先创建一个自定义作用域。有关创建自定义作用域（这是高级任务）的详细信息，请参阅[创建常规或独占作用域](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

有关 Exchange 2013 中管理角色作用域和分配的详细信息，请参阅下列主题：

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

## 使用 EAC 更改角色组上的作用域

在使用 EAC 更改某个角色组上的作用域时，你实际更改的是该角色组与分配给该角色组的每个管理角色之间所有角色分配上的作用域。如果你要更改特定角色分配上的作用域，则必须使用本主题后面的命令行管理程序步骤。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>对于角色与角色组之间的角色分配，如果你使用命令行管理程序在这些角色分配上配置了多个作用域或独占作用域，则不能使用 EAC 管理这些角色分配上的作用域。如果你在这些角色分配上配置了多个作用域或独占作用域，则必须使用本主题后面的命令行管理程序步骤管理这些作用域。有关管理角色作用域的详细信息，请参阅<a href="understanding-management-role-scopes-exchange-2013-help.md">了解管理角色作用域</a>。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  选择要更改其作用域的角色组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  从以下两个\&quot;写入作用域\&quot;选项中选择一个：
    
      - 下拉框中的写入作用域，您可从中选择默认的写入作用域或自定义的写入作用域。
    
      - **组织单位**   如果想要将此角色组的作用域设定为某个组织单位 (OU)，则选择此选项并提供 OU。

4.  单击\&quot;保存\&quot;以保存对角色组的更改。

## 使用命令行管理程序同时更改角色组上所有角色分配的作用域

角色组与分配给它的角色之间的角色分配可以使用从角色本身获取的隐式作用域、相同的自定义作用域或不同的自定义作用域。有关角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

角色分配上的作用域使用 **Set-ManagementRoleAssignment** cmdlet 进行管理。不能使用 **Set-RoleGroup** cmdlet 管理作用域。

若要同时更改角色组与管理角色组之间所有角色分配的作用域，需要首先检索该角色组上的角色分配，然后在每个分配上设置新作用域。通过使用 **Get-ManagementRoleAssignment** cmdlet 来检索角色分配，然后将这些角色分配用管道传递到 **Set-ManagementRoleAssignment** cmdlet 以完成上述更改操作。

此过程使用管道传输和 *WhatIf* 开关的概念。有关详细信息，请参阅下列主题：

  - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))

  - [WhatIf、Confirm 和 ValidateOnly 开关](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

若要同时设置角色组的所有角色分配的作用域，请使用以下语法。

    Get-ManagementRoleAssignment -RoleAssignee <name of role group> | Set-ManagementRoleAssignment -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>

仅使用配置要使用的作用域时所需的参数。例如，如果要将 Sales Recipient Management 角色组上的所有角色分配的收件人作用域更改为 Direct Sales Employees，请使用以下命令。

    Get-ManagementRoleAssignment -RoleAssignee "Sales Recipient Management" | Set-ManagementRoleAssignment -CustomRecipientWriteScope "Direct Sales Employees"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可以使用 <em>WhatIf</em> 开关来验证仅更改了你要更改的角色分配。使用 <em>WhatIf</em> 开关运行上述命令以验证结果，然后删除 <em>WhatIf</em> 开关以应用更改。</td>
</tr>
</tbody>
</table>


有关更改管理角色分配的详细信息，请参阅[更改角色分配](change-a-role-assignment-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 使用命令行管理程序更改角色组上单个角色分配的作用域

角色组与分配给它的角色之间的角色分配可以使用从角色本身获取的隐式作用域、相同的自定义作用域或不同的自定义作用域。有关角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

角色分配上的作用域使用 **Set-ManagementRoleAssignment** cmdlet 进行管理。不能使用 **Set-RoleGroup** cmdlet 管理作用域。

此过程使用管道传输和 **Format-List** cmdlet 的概念。有关详细信息，请参阅下列主题：

  - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))

  - [使用命令输出](working-with-command-output-exchange-2013-help.md)

若要更改角色组与管理角色之间的角色分配上的作用域，首先要找到该角色分配的名称，然后在该角色分配上设置作用域。

1.  若要查找角色组上所有角色分配的名称，请使用以下命令。通过将管理角色分配通过管道传递到 **Format-List** cmdlet，可以查看该分配的完整名称。
    
        Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-List Name

2.  查找要更改的角色分配的名称。请在下一步中使用该角色分配的名称。

3.  若要在单个分配上设置作用域，请使用以下语法。
    
        Set-ManagementRoleAssignment <role assignment name> -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>

仅使用配置要使用的作用域时所需的参数。例如，如果要将 Mail Recipients\_Sales Recipient Management 角色分配的收件人作用域更改为 All Sales Employees，请使用以下命令。

    Set-ManagementRoleAssignment "Mail Recipients_Sales Recipient Management" -CustomRecipientWriteScope "All Sales Employees"

有关更改管理角色分配的详细信息，请参阅[更改角色分配](change-a-role-assignment-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335173\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功更改角色组上角色分配的作用域，请执行以下操作：

  - 如果已使用 EAC 配置角色组上的作用域，则执行以下操作：
    
    1.  在 EAC 中，导航到\&quot;**权限**\&quot;\>\&quot;**管理员角色**\&quot;。这里列出了组织中的所有角色组。
    
    2.  选择某个角色组，以查看该角色组上配置的作用域。

  - 如果已使用命令行管理程序配置角色组上的作用域，则执行以下操作：
    
    1.  在命令行管理程序中运行以下命令。
        
            Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-Table *WriteScope
    
    2.  验证角色分配上的写入作用域是否已更改为您指定的作用域。

## 添加或删除角色组委派

角色组委派是指可以向角色组中添加或从中删除成员或更改角色组属性的用户或通用安全组 (USG)。通过添加或删除角色组委派，可以控制允许哪个用户管理角色组。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>向角色组添加委派之后，该角色组将只能由该角色组上的委派进行管理，或由直接或间接获得 Role Management 管理角色的用户进行管理。<br />
如果用户已直接或间接获得 Role Management 角色，但尚未添加为该角色组的委派，则该用户必须使用 <strong>Add-RoleGroupMember</strong>、<strong>Remove-RoleGroupMember</strong>、<strong>Update-RoleGroupMember</strong> 和 <strong>Set-RoleGroup</strong> cmdlet 上的 <em>BypassSecurityGroupManagerCheck</em> 开关来管理角色组。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不能使用 EAC 将委派添加到角色组。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序将委派添加到角色组

若要更改角色组上的委派列表，请在 **Set-RoleGroup** cmdlet 中使用 *ManagedBy* 参数。*ManagedBy* 参数重写角色组上的整个委派列表。如果你想要将委派添加到角色组而不是替换整个委派列表，请按以下步骤操作：

1.  使用以下命令将角色组存储在一个变量中。
    
        $RoleGroup = Get-RoleGroup <role group name>

2.  使用以下命令将委派添加到存储在变量中的角色组。
    
        $RoleGroup.ManagedBy += (Get-User <user to add>).Identity
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果要添加 USG，请使用 <strong>Get-Group</strong> cmdlet。</td>
    </tr>
    </tbody>
    </table>


3.  请对要添加的每个委派重复步骤 2。

4.  使用以下命令将新的委派列表应用于实际的角色组。
    
        Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy

本示例将用户 David Strome 添加为 组织管理 角色组上的一个委派。

    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy += (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy

有关语法和参数的详细信息，请参阅 [Set-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638182\(v=exchg.150\))。

## 使用命令行管理程序将委派从角色组中删除

若要更改角色组上的委派列表，请在 **Set-RoleGroup** cmdlet 中使用 *ManagedBy* 参数。*ManagedBy* 参数重写角色组上的整个委派列表。如果你想要将委派从角色组中删除而不是替换整个委派列表，请按以下步骤操作：

1.  使用以下命令将角色组存储在一个变量中。
    
        $RoleGroup = Get-RoleGroup <role group name>

2.  使用以下命令将委派从存储在变量中的角色组中删除。
    
        $RoleGroup.ManagedBy -= (Get-User <user to remove>).Identity
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果要删除 USG，请使用 <strong>Get-Group</strong> cmdlet。</td>
    </tr>
    </tbody>
    </table>


3.  请对要删除的每个委派重复步骤 2。

4.  使用以下命令将新的委派列表应用于实际的角色组。
    
        Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy

本示例将作为 组织管理 角色组上委派的用户 David Strome 删除。

    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy -= (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy

有关语法和参数的详细信息，请参阅 [Set-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638182\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功更改角色组上的委派列表，请执行以下操作：

1.  在此命令行管理程序中，运行以下命令。
    
        Get-RoleGroup <role group name> | Format-List ManagedBy

2.  验证 *ManagedBy* 属性上列出的委派是否只包括能够管理角色组的委派。

