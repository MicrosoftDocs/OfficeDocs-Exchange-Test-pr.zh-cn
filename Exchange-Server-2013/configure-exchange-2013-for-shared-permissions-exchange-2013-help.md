---
title: '为 Exchange 2013 配置共享权限: Exchange 2013 Help'
TOCTitle: 为 Exchange 2013 配置共享权限
ms:assetid: 7d119977-b420-4b66-acf0-0a978b188cdd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638146(v=EXCHG.150)
ms:contentKeyID: 50490899
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为 Exchange 2013 配置共享权限

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

共享权限使您（作为 Microsoft Exchange Server 2013 管理员）可以创建 Active Directory 安全主体（如用户），然后将这些安全主体配置为 Exchange 收件人。与拆分权限不同，拆分权限是在 Exchange 管理员组和 Active Directory 管理员组之间分离管理任务，而使用共享权限则不会分离任务。

有关共享和拆分权限的详细信息，请参阅[了解拆分权限](understanding-split-permissions-exchange-2013-help.md)。

如果您之前为您的组织设置了拆分权限，则可以为您的 Exchange 2013 组织配置共享权限。根据您当前使用的是基于角色的访问控制 (RBAC) 拆分权限还是 Active Directory 拆分权限，切换到共享权限的过程会有所不同。选择以下适用于您的当前配置的过程。如果符合以下条件，则您的组织使用的是 Active Directory 拆分权限：

  - 存在 Microsoft Exchange 保护组组织单位 (OU)。

  - Exchange Windows 权限安全组位于 Microsoft Exchange 保护组 OU 中。

  - Exchange 受信任子系统安全组是 Exchange Windows 权限安全组的成员。

  - 没有针对\&quot;邮件收件人创建\&quot;角色和\&quot;安全组创建和成员身份\&quot;角色的常规管理角色分配。

如果您从未为您的组织配置过拆分权限，则无需执行此流程。Exchange 2013 默认配置有共享权限。

有关管理角色组、管理角色以及常规和委派管理角色分配的详细信息，请参阅下列主题：

  - [了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)

  - [了解管理角色组](understanding-management-role-groups-exchange-2013-help.md)

  - [了解管理角色](understanding-management-roles-exchange-2013-help.md)

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

若要了解与权限相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 必须使用 Windows PowerShell 和/或 Windows 命令的命令行管理程序才能执行这些过程。有关详细信息，请参阅每个过程。

  - 当前必须已为 RBAC 或 Exchange 2013 拆分权限配置了 Active Directory 组织。

  - 如果您的组织中具有 Microsoft Exchange Server 2010 服务器，则您选择的权限模型也将应用于这些服务器。

  - 您必须拥有将\&quot;邮件收件人创建\&quot;管理角色和\&quot;安全组创建和成员身份\&quot;管理角色委派给 组织管理 管理角色组或另一个分配了\&quot;邮件收件人\&quot;角色的角色组的权限。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 从 RBAC 拆分权限切换到共享权限

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;角色组\&quot;条目。

要从 RBAC 拆分权限切换到 Exchange 2013 共享权限，必须将\&quot;邮件收件人创建\&quot;角色和\&quot;安全组创建和成员身份\&quot;角色分配给这样一个角色组：该角色组也已经分配了\&quot;邮件收件人\&quot;角色并且成员之中包括 Exchange 2013 管理员。在默认共享权限配置中，组织管理 角色组包含上述所有角色。因此，此过程将使用 组织管理 角色组。

## 配置共享权限

若要在 组织管理 角色组上配置共享权限，请使用特定帐户执行以下操作，该帐户必须拥有委派\&quot;邮件收件人创建\&quot;角色和\&quot;安全组创建和成员身份\&quot;角色的角色分配的权限：

1.  使用以下命令向 组织管理 角色组添加\&quot;邮件收件人创建\&quot;角色和\&quot;安全组创建和成员身份\&quot;角色的委派角色分配。
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management" -Delegating
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management" -Delegating
    
    > [!NOTE]  
    > 必须为包含&amp;quot;邮件收件人创建&amp;quot;角色和&amp;quot;安全组创建和成员身份&amp;quot;角色的委派角色分配的角色组（此过程中的 Active Directory 管理员角色组）分配&amp;quot;角色管理&amp;quot;角色来运行 <strong>New-ManagementRoleAssignment</strong> cmdlet。可以委派&amp;quot;角色管理&amp;quot;角色的角色受理人必须将该角色分配给 Active Directory 管理员角色组。


2.  使用以下命令向 组织管理 和 收件人管理 角色组添加\&quot;邮件收件人创建\&quot;角色的常规角色分配。
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Recipient Management"

3.  使用以下命令向 组织管理 角色组添加\&quot;安全组创建和成员身份\&quot;角色的常规角色分配。
    
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 删除 Active Directory 管理员的权限（可选）

如果不再希望 Active Directory 管理员能够使用 Exchange 管理工具创建或管理 Active Directory 对象，您可以选择删除授予他们的权限。如果要删除 Active Directory 管理员的权限，请执行此过程。

> [!NOTE]  
> 虽然您可以删除 Active Directory 管理员的权限，使其不能使用 Exchange 管理工具管理 Active Directory 对象，但如果其 Active Directory 权限允许，Active Directory 管理员仍可以继续使用 Active Directory 管理工具管理 Active Directory 对象。然而，他们将无法管理 Active Directory 对象上特定于 Exchange 的属性。有关详细信息，请参阅<a href="understanding-split-permissions-exchange-2013-help.md">了解拆分权限</a>。


若要删除 Active Directory 管理员与 Exchange 相关的拆分权限，请执行下列操作：

1.  使用以下命令删除将\&quot;邮件收件人创建\&quot;角色分配给成员之中包含 Active Directory 管理员的角色组或通用安全组 (USG) 的常规角色分配和委派角色分配。此命令使用 Active Directory 管理员角色组作为一个示例。*WhatIf* 开关使您能够看到将删除哪些角色分配。删除 *WhatIf* 开关，然后再次运行命令来删除角色分配。
    
        Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

2.  使用以下命令删除将\&quot;安全组创建和成员身份\&quot;角色分配到包含 Active Directory 管理员成员的角色组或 USG 的常规角色分配和委派角色分配。此命令使用 Active Directory 管理员角色组作为一个示例。*WhatIf* 开关使您能够看到将删除哪些角色分配。删除 *WhatIf* 开关，然后再次运行命令来删除角色分配。
    
        Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

3.  可选。如果要删除 Active Directory 管理员的所有 Exchange 权限，您可以删除这些管理员作为其中成员的角色组或 USG。有关如何删除角色组的详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\)) 和 [Remove-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351205\(v=exchg.150\))。

## 从 Active Directory 拆分权限切换到共享权限

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;Active Directory 拆分权限\&quot;条目。

要从 Active Directory 拆分权限切换到 Exchange 2013 共享权限，必须重新运行 Exchange 安装以在 Active Directory 组织中禁用 Exchange 拆分权限，然后在角色组与\&quot;邮件收件人创建\&quot;角色和\&quot;安全组创建和成员身份\&quot;角色之间创建角色分配。在默认共享权限配置中，组织管理 角色组包含上述所有角色。因此，此过程将使用 组织管理 角色组。

> [!IMPORTANT]  
> 此过程中的 setup.com 命令对 Active Directory 进行更改。必须使用具有进行这些更改所需的权限的帐户。此帐户不能是有权使用 <strong>New-ManagementRoleAssignment</strong> cmdlet 创建角色分配的帐户。使用具有成功完成这一过程的每一步骤所需的权限的帐户。


要从 Active Directory 拆分权限切换到共享权限，请执行以下操作：

1.  从 Windows 命令的命令行管理程序，从 Exchange 2013 安装媒体运行以下命令来禁用 Active Directory 拆分权限。
    
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false

2.  从 Exchange 命令行管理程序，运行以下命令来添加\&quot;邮件收件人创建\&quot;角色和\&quot;安全组创建和成员身份\&quot;角色与 组织管理 及 收件人管理 角色组之间的常规角色分配。
    
        New-ManagementRoleAssignment "Mail Recipient Creation_Organization Management" -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Security Group Creation and Membership_Org Management" -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Mail Recipient Creation_Recipient Management" -Role "Mail Recipient Creation" -SecurityGroup "Recipient Management"

3.  重新启动组织中的 Exchange 2013 服务器。
    
    > [!NOTE]  
    > 如果您组织中有 Exchange 2010 服务器，则还需要重启这些服务器。


有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

