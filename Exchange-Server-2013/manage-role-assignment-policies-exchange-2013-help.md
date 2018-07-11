---
title: '管理角色分配策略: Exchange 2013 Help'
TOCTitle: 管理角色分配策略
ms:assetid: f93d502e-5df4-4ba0-b68d-01a17ccffb4d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657511(v=EXCHG.150)
ms:contentKeyID: 50491980
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理角色分配策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-10-09_

如果您要自定义分配给最终用户组的权限，则创建新的自定义管理角色分配策略。您可以根据最终用户的具体要求自定义要创建的分配策略。 有关 Microsoft Exchange Server 2013 中的分配策略的详细信息，请参阅[了解管理角色分配策略](understanding-management-role-assignment-policies-exchange-2013-help.md)。

是否正在寻找与管理权限相关的其他管理任务？请查看[权限](permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的“分配策略”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 添加分配策略

创建完新的分配策略后，可为其分配用户。 有关详细信息，请参阅[更改邮箱的分配策略](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)。

## 使用 EAC 创建新分配策略

> [!NOTE]  
> 使用 Exchange 管理中心 (EAC) 只能创建显式分配策略。如果要创建新的默认分配策略，则必须使用 Exchange 命令行管理程序。有关详细信息，请参阅本主题后面的“使用命令行管理程序创建默认分配策略”部分。


1.  在 EAC 中，导航至“权限”\>“使用角色”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在角色分配策略窗口，提供新分配策略的名称。

3.  选中要添加到此分配策略的一个或多个角色旁边的复选框。您可以选择多个角色，其中可以包括已添加的最终用户角色。如果选择具有子角色的角色，则会自动选择其子角色。

4.  单击“保存”保存对此分配策略的更改。

## 使用命令行管理程序创建显式分配策略

若要创建可手动分配给邮箱的显式分配策略，请使用以下语法。

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign>

本示例将创建显式分配策略 Limited Mailbox Configuration，并将 `MyBaseOptions`、`MyAddressInformation` 和 `MyDisplayName` 角色分配给它。

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName

有关语法和参数的详细信息，请参阅 [New-RoleAssignmentPolicy](https://technet.microsoft.com/zh-cn/library/dd638101\(v=exchg.150\))。

## 使用命令行管理程序创建默认分配策略

若要创建分配给新邮箱的默认分配策略，请使用以下语法。

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign> -IsDefault

本示例将创建默认分配策略 Limited Mailbox Configuration，并将 `MyBaseOptions`、`MyAddressInformation` 和 `MyDisplayName` 角色分配给它。

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName -IsDefault

有关语法和参数的详细信息，请参阅 [New-RoleAssignmentPolicy](https://technet.microsoft.com/zh-cn/library/dd638101\(v=exchg.150\))。

## 删除分配策略

如果不再需要某个管理角色分配策略，可以将其删除。

## 在开始之前，您需要知道什么？

  - 必须将分配了该分配策略的所有用户更改为其他分配策略。有关如何更改邮箱的分配策略的详细信息，请参阅[更改邮箱的分配策略](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)。

  - 必须删除该分配策略和分配的管理角色之间的所有管理角色分配。 有关如何删除分配策略中的角色分配的详细信息，请参阅本主题稍后的使用命令行管理程序从分配策略中删除角色部分。

  - 如果要删除默认的分配策略，该策略必须是 Exchange 2013 组织中的最后一个分配策略。

## 使用 EAC 删除分配策略

1.  在 EAC 中，导航到“权限” \> “用户角色”。

2.  选择要删除的分配策略，然后单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

## 使用命令行管理程序删除分配策略

若要删除分配策略，请使用以下语法。

    Remove-RoleAssignmentPolicy <role assignment policy>

此示例删除 New York Temporary Users 分配策略。

    Remove-RoleAssignmentPolicy "New York Temporary Users"

有关语法和参数的详细信息，请参阅 [Remove-RoleAssignmentPolicy](https://technet.microsoft.com/zh-cn/library/dd638190\(v=exchg.150\))。

## 查看分配策略列表或分配策略详细信息

可以以多种方式查看管理角色分配策略，这取决于要查看的信息以及是否使用了 EAC 或命令行管理程序。

在 EAC 中，可以查看分配策略列表和分配给它们的角色。在命令行管理程序中，可以查看组织中的所有分配策略、列出分配有特定策略的邮箱以及其他操作。

## 使用 EAC 查看分配策略列表

1.  在 EAC 中，导航到“权限” \> “用户角色”。这里列出了组织中的所有分配策略。

2.  要查看特定分配策略的详细信息，请选择要查看的分配策略。分配策略的说明和分配的角色显示在详细信息窗格中。

## 使用命令行管理程序查看分配策略列表

通过在运行 **Get-RoleAssignmentPolicy** cmdlet 时不指定任何分配策略，您可以查看组织中所有分配策略的列表。

此过程使用了管道传输和 **Format-Table** cmdlet。有关这些概念的详细信息，请参阅以下主题：

  - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))

  - [使用命令输出](working-with-command-output-exchange-2013-help.md)

若要返回组织中所有分配策略的列表，请使用以下命令。

    Get-RoleAssignmentPolicy

若要返回组织中所有分配策略的特定属性列表，可将结果通过管道传递给 **Format-Table** cmdlet 并在结果列表中指定所需的属性。请使用以下语法：

    Get-RoleAssignmentPolicy | Format-Table <property 1>, <property 2...>

本示例将返回组织中所有分配策略的列表，其中包括 **Name** 和 **IsDefault** 属性。

    Get-RoleAssignmentPolicy | Format-Table Name, IsDefault

有关语法和参数的详细信息，请参阅 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) 和 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/zh-cn/library/dd638195\(v=exchg.150\))。

## 使用命令行管理程序查看单个分配策略的详细信息

可通过使用 **Get-RoleAssignmentPolicy** cmdlet 并将输出通过管道传递给 **Format-List** cmdlet，来查看特定分配策略的详细信息。

此过程使用了管道传输和 **Format-List** cmdlet。有关这些概念的详细信息，请参阅以下主题：

  - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))

  - [使用命令输出](working-with-command-output-exchange-2013-help.md)

若要查看特定分配策略的详细信息，请使用以下语法。

    Get-RoleAssignmentPolicy <assignment policy name> | Format-List

本示例可查看 Redmond Users - no Text Messaging 分配策略的详细信息。

    Get-RoleAssignmentPolicy "Redmond Users - no Text Messaging" | Format-List

有关语法和参数的详细信息，请参阅 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) 和 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/zh-cn/library/dd638195\(v=exchg.150\))。

## 使用命令行管理程序查找默认分配策略

可通过以下方法查找默认分配策略：将 **Get-RoleAssignmentPolicy** cmdlet 的输出通过管道传递给 **Where** cmdlet。使用 **Where** cmdlet 筛选返回的数据，以便仅显示 *IsDefault* 设为 `$True` 的分配策略。

此过程使用了管道传输和 **Where** cmdlet。有关这些概念的详细信息，请参阅以下主题：

  - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))

  - [使用命令输出](working-with-command-output-exchange-2013-help.md)

本示例将返回默认分配策略。

    Get-RoleAssignmentPolicy | Where { $_.IsDefault -eq $True }

有关语法和参数的详细信息，请参阅 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) 和 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/zh-cn/library/dd638195\(v=exchg.150\))。

## 使用命令行管理程序查看分配了特定策略的邮箱

可通过以下方法查找所有分配了特定分配策略的邮箱：将 **Get-Mailbox** cmdlet 的输出通过管道传递给 **Where** cmdlet。使用 **Where** cmdlet 筛选返回的数据，以便仅显示 *RoleAssignmentPolicy* 属性已设为所指定分配策略名称的邮箱。

此过程使用了管道传输和 **Where** cmdlet。有关这些概念的详细信息，请参阅以下主题：

  - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))

  - [使用命令输出](working-with-command-output-exchange-2013-help.md)

请使用以下语法：

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<role assignment policy>" }

本示例将查找所有分配了策略 Vancouver End Users 的邮箱。

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Vancouver End Users" }

有关语法和参数的详细信息，请参阅 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) 和 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/zh-cn/library/dd638195\(v=exchg.150\))。

## 更改默认分配策略

您可以更改为新创建的邮箱分配的管理角色分配策略。 更改默认角色分配策略将不会更改分配给现有邮箱的分配策略。要更改分配给现有邮箱的分配策略，请参阅[更改邮箱的分配策略](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)。

> [!NOTE]  
> 不能使用 EAC 更改默认分配策略。 需要使用命令行管理程序。


## 使用命令行管理程序更改默认分配策略

若要更改默认分配策略，请使用以下语法。

    Set-RoleAssignmentPolicy <assignment policy name> -IsDefault

此示例将 Vancouver 最终用户分配策略设置为默认分配策略。

    Set-RoleAssignmentPolicy "Vancouver End Users" -IsDefault

> [!IMPORTANT]  
> 将为新邮箱分配默认分配策略，即使此策略尚未分配管理角色也是如此。 邮箱分配的未分配管理角色的分配策略无法访问 Microsoft Outlook Web App 中的任何邮箱配置功能。


有关语法和参数的详细信息，请参阅 [Set-RoleAssignmentPolicy](https://technet.microsoft.com/zh-cn/library/dd638090\(v=exchg.150\))。

## 向分配策略添加角色

## 使用 EAC 向分配策略添加角色

1.  在 EAC 中，导航到“权限” \> “用户角色”。

2.  选择要向其添加一个或多个角色的分配策略，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  选中要添加到此分配策略的一个或多个角色旁边的复选框。您可以选择多个角色，其中可以包括已添加的最终用户角色。如果选择具有子角色的角色，则会自动选择其子角色。

4.  单击“保存”保存对此分配策略的更改。

## 使用命令行管理程序向分配策略中添加角色

若要在角色与分配策略之间创建管理角色分配，请使用以下语法。

    New-ManagementRoleAssignment -Name <role assignment name> -Role <role name> -Policy <assignment policy name>

本示例在 MyVoicemail 角色与 Seattle Users 分配策略之间创建角色分配 Seattle Users - Voicemail。

    New-ManagementRoleAssignment -Name "Seattle Users - Voicemail" -Role MyVoicemail -Policy "Seattle Users"

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 从分配策略中删除角色

如果您不希望最终用户拥有管理其邮箱或通讯组的特定功能的权限，则可以从为该用户分配的管理角色分配策略中删除授予权限的管理角色。如果将同一分配策略分配给其他用户，他们也将无法管理该功能。

## 使用 EAC 从分配策略中删除角色

1.  在 EAC 中，导航到“权限” \> “用户角色”。

2.  选择要从其中删除一个或多个角色的分配策略，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  清除要从分配策略中删除的一个或多个角色旁边的复选框。如果清除具有子角色的角色对应的复选框，则同时还会清除其子角色对应的复选框。

4.  单击“保存”保存对此分配策略的更改。

## 使用命令行管理程序从分配策略中删除角色

您可以通过使用 **Get-ManagementRoleAssignment** cmdlet 检索关联管理角色分配，然后通过管道将返回的角色分配传输到 **Remove-ManagementRoleAssignment** cmdlet，来将角色从分配策略中删除。

有关常规角色分配和委派角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

此过程使用管道进行传输。有关管道传输的详细信息，请参阅[管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))。

若要从分配策略中删除角色，请使用以下语法。

    Get-ManagementRoleAssignment -RoleAssignee <assignment policy name> -Role <role name> | Remove-ManagementRoleAssignment

本示例将从 Seattle Users 分配策略中删除 MyVoicemail 管理角色，该角色使用户能够管理其语音邮件选项。

    Get-ManagementRoleAssignment -RoleAssignee "Seattle Users" -Role MyVoicemail | Remove-ManagementRoleAssignment

有关语法和参数的详细信息，请参阅 [Remove-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351205\(v=exchg.150\))。

