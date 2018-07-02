---
title: '更改顶级未区分范围角色的角色条目: Exchange 2013 Help'
TOCTitle: 更改顶级未区分范围角色的角色条目
ms:assetid: 65c0bfb3-aafd-4c64-8429-7616c57adf1c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876896(v=EXCHG.150)
ms:contentKeyID: 50490732
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更改顶级未区分范围角色的角色条目

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

未区分范围顶级管理角色的管理角色条目引用脚本和非Exchange cmdlet 和其参数，要使可供分配的角色。通过更改角色条目上可用的参数，您可以控制哪些分配与非Exchange cmdlet 的脚本可以执行的任务。有关未区分范围的角色条目的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要更改包含 Exchange cmdlet 的管理角色的角色条目，请参阅<a href="change-a-role-entry-exchange-2013-help.md">更改角色条目</a>。</td>
</tr>
</tbody>
</table>


若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理角色\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 默认情况下不包含任何管理角色组中更改未区分范围的顶级角色的角色条目的能力。您必须首先将未区分范围角色管理角色到用户，或通用安全组 (USG) 或用户是其成员，用户可添加或更改一个未区分范围顶级角色条目之前的角色组。有关添加角色到用户、 USG 或角色组的详细信息，请参阅下列主题 ︰
    
      - [管理角色组](manage-role-groups-exchange-2013-help.md)
    
      - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

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

## 使用命令行管理程序向角色条目添加一个或多个参数

若要将参数添加到无作用域的顶级角色条目中，需要执行下列操作：

  - 使用 *Parameters* 参数指定要添加的参数。

  - 指定 *AddParameter* 参数表示要执行添加操作。

  - 指定*UnscopedTopLevel*参数，以指示您要更改未区分范围的顶级角色上的角色项。如果不指定此参数，未区分范围角色的角色项更改时，将发生错误。

若要向角色条目添加参数，请使用以下语法。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter -UnscopedTopLevel

本示例将 *EmailAddress* 和 *City* 参数添加到 Recipient Administrators 无作用域角色上的 **CreateUsers.ps1** 脚本。

    Set-ManagementRoleEntry "Recipient Administrators\CreateUsers.ps1" -Parameters EmailAddress, City -AddParameter -UnscopedTopLevel

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351162\(v=exchg.150\))。

## 使用命令行管理程序删除角色条目中的一个或多个参数

若要从角色条目中删除参数，需要执行下列操作：

  - 使用 *Parameters* 参数指定要删除的参数。

  - 指定 *RemoveParameter* 参数表示要执行删除操作。

  - 指定*UnscopedTopLevel*参数，以指示您要更改未区分范围的顶级角色上的角色项。如果不指定此参数，未区分范围角色的角色项更改时，将发生错误。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您不能撤消删除操作。如果您误删除角色条目中的参数，则必须再次手动添加它。</td>
</tr>
</tbody>
</table>


若要删除角色条目中的参数，请使用以下语法。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter -UnscopedTopLevel

本示例将 *Delay*、*Force* 及 *Credential* 参数从 Tier 1 Server Administrators 角色上的 **Start-Widget** 非 Exchange cmdlet 中删除。

    Set-ManagementRoleEntry "Tier 1 Server Administrators\Start-Widget" -Parameters Delay, Force, Credential -RemoveParameter -UnscopedTopLevel

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351162\(v=exchg.150\))。

## 使用命令行管理程序删除角色条目中的所有参数

若要从角色条目中删除所有参数，需要执行下列操作：

  - 在*Parameters*参数中指定值`$Null` 。您不需要使用*RemoveParameter*参数。

  - 指定*UnscopedTopLevel*参数，以指示您要更改未区分范围的顶级角色上的角色项。如果不指定此参数，未区分范围角色的角色项更改时，将发生错误。

若要仅使少数参数在脚本或非 Exchange cmdlet 上可用并排除其他所有参数时，从角色条目中删除所有参数最为有用。

如果您不想要有权访问脚本或非Exchange cmdlet 的角色，而只删除参数不是完全在角色中删除关联的角色条目。有关如何从角色中删除一个角色条目的详细信息，请参阅[从角色中删除一个角色条目](remove-a-role-entry-from-a-role-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您不能撤消删除操作。如果错误地从角色条目中删除所有参数，您必须再次手动添加它们。</td>
</tr>
</tbody>
</table>


若要删除角色条目中的所有参数，请使用以下语法。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters $Null -UnscopedTopLevel

本示例将从 Recipient Administrators 角色上的 FindMailboxesOverQuota.ps1 脚本中删除所有参数。

    Set-ManagementRoleEntry "Recipient Administrators\FindMailboxesOverQuota.ps1" -Parameters $Null -UnscopedTopLevel

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351162\(v=exchg.150\))。

## 使用命令行管理程序应用特定的一组参数

若要使角色条目中仅包括一组特定的参数，需要执行下列操作：

  - 指定*Parameters*参数只。不要包含*AddParameter*或*RemoveParameter*参数。

  - 指定*UnscopedTopLevel*参数，以指示您要更改未区分范围角色上的角色项。如果不指定此参数，未区分范围的顶级角色的角色项更改时，将发生错误。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>指定只有<em>Parameters</em>参数时，只在命令中指定的参数包含在角色条目。所有其它参数将被移除。</td>
</tr>
</tbody>
</table>


若要指定一组特定的参数，请使用以下语法。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -UnscopedTopLevel

本示例仅包括 Seattle Mail Recipient Admins 角色上 **Set-Widget** cmdlet 中的 *Alias*、*DisplayName*、*WidgetConfig* 和 *Enabled* 参数。

    Set-ManagementRoleEntry "Seattle Mail Recipient Admins\Set-UMMailbox" -Parameters Alias, DisplayName, WidgetConfig, Enabled -UnscopedTopLevel

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351162\(v=exchg.150\))。

## 其他任务

在更改无作用域顶级角色上的角色条目之后，您可能还需要：

[向角色添加角色](add-a-role-entry-to-a-role-exchange-2013-help.md)

[管理角色组](manage-role-groups-exchange-2013-help.md)

[管理角色组成员](manage-role-group-members-exchange-2013-help.md)

[向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[从用户或 USG 删除角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

